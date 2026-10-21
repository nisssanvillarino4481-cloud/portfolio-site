# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.

###!/usr/bin/env python3

"""
AI-ASTRA Security Engine
ULTRAMAX OMEGA SHIELD — Security Enforcement Core

Purpose:
- Local authentication
- Authorization / policy checks
- Request validation
- Rate limiting
- Security event logging
- Health/status reporting
- Fail-closed behavior for protected operations

This module is intentionally defensive.
It does NOT execute arbitrary commands, modify project files,
or automatically take destructive actions.
"""

from __future__ import annotations

import hashlib
import hmac
import json
import os
import threading
import time
from collections import defaultdict, deque
from datetime import datetime, timezone
from pathlib import Path
from typing import Any, Dict, Optional


# ---------------------------------------------------------------------
# PATHS
# ---------------------------------------------------------------------

BASE_DIR = Path(__file__).resolve().parents[2]

LOG_DIR = BASE_DIR / "logs" / "security"
EVENT_LOG = LOG_DIR / "events.log"
AUDIT_LOG = LOG_DIR / "audit.log"

LOG_DIR.mkdir(parents=True, exist_ok=True)


# ---------------------------------------------------------------------
# CONFIGURATION
# ---------------------------------------------------------------------

ENGINE_NAME = "ULTRAMAX-OMEGA-SHIELD"
ENGINE_VERSION = "1.0"

MAX_REQUESTS_PER_MINUTE = 60
MAX_BODY_SIZE = 1024 * 1024  # 1 MB

LOCK = threading.RLock()

_REQUESTS = defaultdict(deque)


# ---------------------------------------------------------------------
# TIME
# ---------------------------------------------------------------------

def utc_now() -> str:
    """Return an ISO-8601 UTC timestamp."""
    return datetime.now(timezone.utc).isoformat()


# ---------------------------------------------------------------------
# LOGGING
# ---------------------------------------------------------------------

def _write_log(path: Path, event: Dict[str, Any]) -> None:
    """Append one JSON security event to a log file."""
    line = json.dumps(event, ensure_ascii=False, sort_keys=True)

    with LOCK:
        with path.open("a", encoding="utf-8") as handle:
            handle.write(line + "\n")


def security_event(
    event_type: str,
    status: str,
    source: str = "unknown",
    details: Optional[Dict[str, Any]] = None,
) -> Dict[str, Any]:
    """Create and record a security event."""

    event = {
        "timestamp": utc_now(),
        "engine": ENGINE_NAME,
        "version": ENGINE_VERSION,
        "event_type": event_type,
        "status": status,
        "source": source,
        "details": details or {},
    }

    _write_log(EVENT_LOG, event)
    return event


def audit_event(
    action: str,
    result: str,
    source: str = "unknown",
    details: Optional[Dict[str, Any]] = None,
) -> Dict[str, Any]:
    """Create and record an audit event."""

    event = {
        "timestamp": utc_now(),
        "engine": ENGINE_NAME,
        "action": action,
        "result": result,
        "source": source,
        "details": details or {},
    }

    _write_log(AUDIT_LOG, event)
    return event


# ---------------------------------------------------------------------
# REQUEST VALIDATION
# ---------------------------------------------------------------------

def validate_request(request: Any) -> tuple[bool, str]:
    """
    Validate a protected request.

    Expected structure:
        {
            "action": "...",
            "source": "...",
            "timestamp": ...,
            "payload": {...}
        }
    """

    if not isinstance(request, dict):
        return False, "request must be an object"

    action = request.get("action")
    source = request.get("source")

    if not isinstance(action, str) or not action.strip():
        return False, "missing action"

    if not isinstance(source, str) or not source.strip():
        return False, "missing source"

    payload = request.get("payload", {})

    if payload is not None and not isinstance(payload, dict):
        return False, "payload must be an object"

    try:
        encoded = json.dumps(
            request,
            ensure_ascii=False,
            separators=(",", ":"),
        ).encode("utf-8")
    except (TypeError, ValueError):
        return False, "request is not serializable"

    if len(encoded) > MAX_BODY_SIZE:
        return False, "request exceeds maximum size"

    return True, "valid"


# ---------------------------------------------------------------------
# RATE LIMITING
# ---------------------------------------------------------------------

def rate_limit(source: str) -> tuple[bool, str]:
    """
    Simple in-memory rate limiter.

    Returns:
        (True, "allowed")
        (False, "rate limit exceeded")
    """

    now = time.monotonic()

    with LOCK:
        bucket = _REQUESTS[source]

        while bucket and now - bucket[0] >= 60:
            bucket.popleft()

        if len(bucket) >= MAX_REQUESTS_PER_MINUTE:
            security_event(
                "RATE_LIMIT",
                "DENIED",
                source,
                {"limit": MAX_REQUESTS_PER_MINUTE},
            )
            return False, "rate limit exceeded"

        bucket.append(now)

    return True, "allowed"


# ---------------------------------------------------------------------
# AUTHENTICATION
# ---------------------------------------------------------------------

def _configured_secret() -> Optional[str]:
    """
    Read the authentication secret from the environment.

    The engine deliberately does NOT hard-code a secret.
    """

    secret = os.environ.get("AI_ASTRA_SECURITY_TOKEN")

    if not secret:
        return None

    return secret


def authenticate(token: Optional[str], source: str) -> tuple[bool, str]:
    """
    Authenticate a request using an environment-provided token.

    No default token is accepted.
    """

    expected = _configured_secret()

    if not expected:
        security_event(
            "AUTHENTICATION",
            "DENIED",
            source,
            {"reason": "security token not configured"},
        )
        return False, "authentication unavailable"

    if not token:
        security_event(
            "AUTHENTICATION",
            "DENIED",
            source,
            {"reason": "missing token"},
        )
        return False, "authentication required"

    if not hmac.compare_digest(str(token), expected):
        security_event(
            "AUTHENTICATION",
            "DENIED",
            source,
            {"reason": "invalid token"},
        )
        return False, "authentication failed"

    security_event(
        "AUTHENTICATION",
        "ALLOWED",
        source,
    )

    return True, "authenticated"


# ---------------------------------------------------------------------
# AUTHORIZATION
# ---------------------------------------------------------------------

# Explicit allow-list.
# Add only trusted internal operations.
ALLOWED_ACTIONS = {
    "health",
    "status",
    "heartbeat",
}


def authorize(action: str, source: str) -> tuple[bool, str]:
    """Authorize a validated action."""

    normalized = action.strip().lower()

    if normalized not in ALLOWED_ACTIONS:
        security_event(
            "AUTHORIZATION",
            "DENIED",
            source,
            {"action": normalized},
        )

        return False, "action not authorized"

    audit_event(
        "authorization",
        "allowed",
        source,
        {"action": normalized},
    )

    return True, "authorized"


# ---------------------------------------------------------------------
# REQUEST SECURITY GATE
# ---------------------------------------------------------------------

def security_gate(
    request: Any,
    token: Optional[str] = None,
) -> Dict[str, Any]:
    """
    Main security decision point.

    Returns a structured result rather than executing the request.
    """

    source = (
        request.get("source", "unknown")
        if isinstance(request, dict)
        else "unknown"
    )

    valid, validation_message = validate_request(request)

    if not valid:
        security_event(
            "VALIDATION",
            "DENIED",
            source,
            {"reason": validation_message},
        )

        return {
            "allowed": False,
            "stage": "validation",
            "reason": validation_message,
        }

    limited, limit_message = rate_limit(source)

    if not limited:
        return {
            "allowed": False,
            "stage": "rate_limit",
            "reason": limit_message,
        }

    authenticated, auth_message = authenticate(token, source)

    if not authenticated:
        return {
            "allowed": False,
            "stage": "authentication",
            "reason": auth_message,
        }

    authorized, authorization_message = authorize(
        request["action"],
        source,
    )

    if not authorized:
        return {
            "allowed": False,
            "stage": "authorization",
            "reason": authorization_message,
        }

    security_event(
        "SECURITY_GATE",
        "ALLOWED",
        source,
        {"action": request["action"]},
    )

    return {
        "allowed": True,
        "stage": "complete",
        "reason": "request authorized",
    }


# ---------------------------------------------------------------------
# HEALTH / STATUS
# ---------------------------------------------------------------------

def health() -> Dict[str, Any]:
    """Return security engine health information."""

    return {
        "engine": ENGINE_NAME,
        "version": ENGINE_VERSION,
        "status": "ACTIVE",
        "authentication_configured": bool(
            _configured_secret()
        ),
        "event_log": str(EVENT_LOG),
        "audit_log": str(AUDIT_LOG),
        "timestamp": utc_now(),
    }


def status() -> Dict[str, Any]:
    """Alias for health status."""

    return health()


# ---------------------------------------------------------------------
# HEARTBEAT
# ---------------------------------------------------------------------

def heartbeat() -> Dict[str, Any]:
    """Record a security-engine heartbeat."""

    event = security_event(
        "HEARTBEAT",
        "OK",
        ENGINE_NAME,
    )

    return {
        "status": "HEARTBEAT OK",
        "timestamp": event["timestamp"],
        "engine": ENGINE_NAME,
    }


# ---------------------------------------------------------------------
# SELF TEST
# ---------------------------------------------------------------------

def self_test() -> Dict[str, Any]:
    """
    Non-destructive internal test.

    This verifies validation and policy behavior without executing
    external commands or modifying project files.
    """

    results = {}

    valid_request = {
        "action": "health",
        "source": "self-test",
        "payload": {},
    }

    invalid_request = {
        "source": "self-test",
        "payload": {},
    }

    valid, message = validate_request(valid_request)
    results["valid_request"] = {
        "passed": valid,
        "message": message,
    }

    invalid, invalid_message = validate_request(invalid_request)
    results["invalid_request_rejected"] = {
        "passed": not invalid,
        "message": invalid_message,
    }

    health_result = health()

    results["health"] = {
        "passed": health_result["status"] == "ACTIVE",
        "status": health_result["status"],
    }

    overall = all(
        item.get("passed", False)
        for item in results.values()
    )

    security_event(
        "SELF_TEST",
        "PASS" if overall else "FAIL",
        ENGINE_NAME,
        results,
    )

    return {
        "engine": ENGINE_NAME,
        "status": "PASS" if overall else "FAIL",
        "results": results,
        "timestamp": utc_now(),
    }


# ---------------------------------------------------------------------
# CLI
# ---------------------------------------------------------------------

if __name__ == "__main__":
    print("=" * 60)
    print(f"{ENGINE_NAME} v{ENGINE_VERSION}")
    print("=" * 60)

    result = self_test()

    print(json.dumps(
        result,
        indent=2,
        ensure_ascii=False,
    ))
