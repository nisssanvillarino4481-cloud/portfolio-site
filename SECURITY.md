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

=========================================
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#070b13">
  <title>ASTRA // Cyber Defense Command</title>
  <link rel="stylesheet" href="styles.css">
  <script src="script.js" defer></script>
</head>
<body>
  <div class="shell">
    <aside class="sidebar" aria-label="Main navigation">
      <a class="brand" href="#overview" aria-label="Astra home">
        <span class="brand-mark">A<span>✳</span></span>
        <span class="brand-copy"><strong>ASTRA</strong><small>DEFENSE NETWORK</small></span>
      </a>
      <div class="nav-label">COMMAND</div>
      <nav>
        <a class="nav-item active" href="#overview"><span>◈</span> Overview</a>
        <a class="nav-item" href="#threats"><span>⌁</span> Threat intelligence <b class="nav-count">4</b></a>
        <a class="nav-item" href="#systems"><span>▦</span> Defense systems</a>
        <a class="nav-item" href="#activity"><span>◷</span> Event timeline</a>
      </nav>
      <div class="sidebar-bottom">
        <div class="operator-card"><div class="operator-icon">●</div><div><strong>Operator mode</strong><small><i class="online-dot"></i> Secure session</small></div><span class="more">···</span></div>
        <div class="sidebar-foot">ASTRA CORE <span>v4.2.0</span></div>
      </div>
    </aside>

    <main class="main-content" id="overview">
      <header class="topbar">
        <div class="breadcrumb">SECURITY OPERATIONS <span>/</span> <strong>OVERVIEW</strong></div>
        <div class="topbar-right"><span class="live-label"><i class="online-dot"></i> ALL SYSTEMS LIVE</span><span class="top-divider"></span><span class="clock" id="currentTime">Loading time…</span><button class="avatar" aria-label="Operator profile">OP</button></div>
      </header>

      <section class="welcome">
        <div><div class="eyebrow"><span class="eyebrow-line"></span> UNIFIED DEFENSE FRAMEWORK</div><h1>Good day, <span>Operator.</span></h1><p>Your environment is being monitored. Here’s your security posture at a glance.</p></div>
        <button class="button button-secondary" id="refreshButton"><span class="refresh-icon">↻</span> Refresh telemetry</button>
      </section>

      <section class="status-banner" aria-label="Security posture">
        <div class="status-emblem"><span>✓</span></div>
        <div class="status-copy"><span class="status-kicker">GLOBAL SECURITY POSTURE</span><strong>All clear <span class="status-pill">NOMINAL</span></strong><small>No critical incidents detected across monitored systems.</small></div>
        <div class="banner-meta"><span>LAST ASSESSMENT</span><strong id="assessmentTime">Just now</strong></div>
        <div class="banner-meta"><span>PROTECTION COVERAGE</span><strong>98.7%</strong></div>
        <div class="banner-spark" aria-hidden="true"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></div>
      </section>

      <section class="metric-grid" aria-label="Security metrics">
        <article class="metric-card"><div class="metric-head"><span>THREATS BLOCKED</span><span class="metric-icon purple">⌁</span></div><div class="metric-value" id="threatsBlocked">2,481</div><div class="metric-foot"><span class="trend positive">↗ 12.8%</span><span>vs. previous 24h</span><svg viewBox="0 0 90 28" aria-hidden="true"><path d="M1 22 C12 19, 13 23, 23 14 S38 19, 48 10 S62 15, 69 7 S80 10, 89 2"/></svg></div></article>
        <article class="metric-card"><div class="metric-head"><span>ACTIVE INCIDENTS</span><span class="metric-icon amber">!</span></div><div class="metric-value">03 <small class="value-unit">under review</small></div><div class="metric-foot"><span class="trend neutral">● Monitored</span><span>0 critical · 3 low</span><svg class="amber-line" viewBox="0 0 90 28" aria-hidden="true"><path d="M1 14 C11 14, 14 10, 23 13 S38 17, 48 12 S64 15, 72 10 S83 12, 89 8"/></svg></div></article>
        <article class="metric-card"><div class="metric-head"><span>NETWORK INTEGRITY</span><span class="metric-icon cyan">⌘</span></div><div class="metric-value">99.98<span class="value-unit">%</span></div><div class="metric-foot"><span class="trend positive">↗ Optimal</span><span>Across 128 nodes</span><svg class="cyan-line" viewBox="0 0 90 28" aria-hidden="true"><path d="M1 17 C10 17, 14 12, 24 15 S36 10, 45 13 S56 11, 66 12 S79 8, 89 7"/></svg></div></article>
        <article class="metric-card"><div class="metric-head"><span>MEAN RESPONSE TIME</span><span class="metric-icon green">ϟ</span></div><div class="metric-value">0.24 <small class="value-unit">sec</small></div><div class="metric-foot"><span class="trend positive">↓ 18ms</span><span>Automated response</span><svg class="green-line" viewBox="0 0 90 28" aria-hidden="true"><path d="M1 5 C12 8, 17 7, 25 12 S38 11, 47 16 S62 13, 72 20 S82 16, 89 23"/></svg></div></article>
      </section>

      <div class="section-heading"><div><h2>Defense network</h2><p>Live status across your protection layers</p></div><a class="text-link" href="#systems">View system details <span>↗</span></a></div>
      <section class="system-grid" id="systems" aria-label="Defense systems">
        <article class="system-card"><div class="system-top"><div class="system-icon icon-violet">◈</div><span class="system-status"><i></i> OPERATIONAL</span></div><h3>Quantum Shield</h3><p>Encryption &amp; secure key management</p><div class="system-bottom"><span>KEY ROTATION</span><strong>Healthy <i class="mini-check">✓</i></strong></div></article>
        <article class="system-card"><div class="system-top"><div class="system-icon icon-blue">⌁</div><span class="system-status"><i></i> OPERATIONAL</span></div><h3>ThreatGlass</h3><p>Real-time threat detection &amp; monitoring</p><div class="system-bottom"><span>FEED STATUS</span><strong>Streaming <i class="mini-check">✓</i></strong></div></article>
        <article class="system-card"><div class="system-top"><div class="system-icon icon-cyan">▤</div><span class="system-status"><i></i> OPERATIONAL</span></div><h3>Defense Grid</h3><p>Intrusion prevention &amp; firewall orchestration</p><div class="system-bottom"><span>POLICY SYNC</span><strong>In sync <i class="mini-check">✓</i></strong></div></article>
        <article class="system-card"><div class="system-top"><div class="system-icon icon-green">⬡</div><span class="system-status"><i></i> OPERATIONAL</span></div><h3>Guardian</h3><p>Compliance, identity &amp; policy enforcement</p><div class="system-bottom"><span>COMPLIANCE</span><strong>98.7% <i class="mini-check">✓</i></strong></div></article>
      </section>

      <section class="lower-grid">
        <article class="panel threat-panel" id="threats"><div class="panel-heading"><div><h2>Threat landscape</h2><p>Detections across the last 24 hours</p></div><span class="select-display">LAST 24 HOURS⌄</span></div><div class="chart-legend"><span><i class="legend-dot purple-dot"></i> Detected threats</span><span><i class="legend-dot cyan-dot"></i> Blocked</span></div><div class="chart" aria-label="Threat detections have remained low and stable"><div class="chart-y"><span>120</span><span>80</span><span>40</span><span>0</span></div><div class="chart-area"><div class="grid-lines"><i></i><i></i><i></i><i></i></div><svg viewBox="0 0 700 150" preserveAspectRatio="none" role="img" aria-label="Line chart showing detected and blocked threats"><defs><linearGradient id="fillPurple" x1="0" x2="0" y1="0" y2="1"><stop offset="0" stop-color="#9b7cff" stop-opacity=".22"/><stop offset="1" stop-color="#9b7cff" stop-opacity="0"/></linearGradient></defs><path class="area-path" d="M0 106 C35 94 48 108 82 87 S135 98 169 71 S220 91 253 68 S305 81 339 52 S391 79 424 63 S476 77 509 47 S560 67 594 37 S650 52 700 25 L700 150 L0 150Z"/><path class="chart-line detected-line" d="M0 106 C35 94 48 108 82 87 S135 98 169 71 S220 91 253 68 S305 81 339 52 S391 79 424 63 S476 77 509 47 S560 67 594 37 S650 52 700 25"/><path class="chart-line blocked-line" d="M0 124 C40 120 51 126 83 111 S135 120 169 101 S219 112 253 94 S306 108 339 84 S390 104 424 89 S478 101 509 76 S560 92 594 68 S650 83 700 54"/></svg><div class="chart-x"><span>00:00</span><span>04:00</span><span>08:00</span><span>12:00</span><span>16:00</span><span>20:00</span><span>NOW</span></div></div></div></article>
        <article class="panel activity-panel" id="activity"><div class="panel-heading"><div><h2>Recent activity</h2><p>Latest security events</p></div><a class="text-link" href="#activity">View all <span>→</span></a></div><div class="activity-list"><div class="activity-item"><span class="activity-mark blocked">⊘</span><div class="activity-detail"><strong>Suspicious connection blocked</strong><small>Edge firewall · 185.220.101.4</small></div><time>2m ago</time></div><div class="activity-item"><span class="activity-mark scan">⌕</span><div class="activity-detail"><strong>Threat scan completed</strong><small>ThreatGlass · No malware found</small></div><time>14m ago</time></div><div class="activity-item"><span class="activity-mark policy">✓</span><div class="activity-detail"><strong>Access policy verified</strong><small>Guardian · 12 policies checked</small></div><time>38m ago</time></div><div class="activity-item"><span class="activity-mark update">↻</span><div class="activity-detail"><strong>Threat intelligence updated</strong><small>Global feed · 1,204 indicators</small></div><time>1h ago</time></div></div></article>
      </section>
      <footer class="footer"><span>ASTRA DEFENSE NETWORK <i>•</i> SECURE BY DESIGN</span><span>Telemetry is simulated for dashboard demonstration</span></footer>
    </main>
  </div>
  <div class="toast" id="toast" role="status" aria-live="polite">Telemetry refreshed</div>
</body>
</html>
