##portfolio-site
##ai-combi-ailoveu
##ai-heart-u
##heart-to-heart-talk
##ai-astra-ph.py
##phillipines_costumer_schema-v1+
##console.log(String.raw`<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Astra Console — Overview</title>
  <link rel="stylesheet" href="/theme.css">
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box
    }

    body {
      margin: 0;
      background: var(--color-bg);
      color: var(--color-text);
      font-family: var(--font-body)
    }

    h1,
    h2,
    h3,
    .brand {
      font-family: var(--font-heading)
    }

    .panel {
      background: var(--color-surface);
      border: 1px solid var(--color-line);
      border-radius: var(--radius)
    }

    .navitem {
      color: var(--color-muted)
    }

    .navitem.active {
      color: var(--color-primary);
      background: rgba(72, 224, 189, .09)
    }

    .navitem:hover {
      color: var(--color-text);
      background: rgba(255, 255, 255, .04)
    }

    @media(max-width:760px) {
      .sidebar {
        display: none
      }

      .mobile-menu {
        display: block !important
      }

      .main-content {
        padding: 22px !important
      }

      .hide-mobile {
        display: none
      }
    }

  </style>
</head>

<body>
  <header class="sticky top-0 z-20 border-b" style="background:rgba(7,17,15,.92);border-color:var(--color-line);backdrop-filter:blur(16px)">
    <div class="mx-auto flex max-w-[1500px] items-center justify-between px-5 py-4 lg:px-8">
      <div class="flex items-center gap-10"><a href="/" class="brand flex items-center gap-3 text-lg font-extrabold"><span class="grid h-9 w-9 place-items-center rounded-xl" style="background:var(--color-primary);color:var(--color-primary-contrast)"><svg width="20" height="20" viewBox="0 0 24 24" fill="none">
              <path d="M12 2.8 20 6v5.1c0 5.2-3.4 8.5-8 10.1-4.6-1.6-8-4.9-8-10.1V6l8-3.2Z" stroke="currentColor" stroke-width="1.8" />
              <path d="m8.7 12.1 2.1 2.1 4.7-4.8" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" />
            </svg></span>astra<span style="color:var(--color-primary)">.</span></a><span class="hidden text-sm md:block" style="color:var(--color-muted)">Workspace <span class="mx-2">/</span> Overview</span></div>
      <div class="flex items-center gap-4"><button class="relative grid h-10 w-10 place-items-center rounded-xl" style="border:1px solid var(--color-line);color:var(--color-muted)"><svg width="18" height="18" viewBox="0 0 24 24" fill="none">
            <path d="M18 9a6 6 0 0 0-12 0c0 7-3 7-3 9h18c0-2-3-2-3-9Zm-8 13h4" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" />
          </svg><span class="absolute right-2 top-2 h-1.5 w-1.5 rounded-full" style="background:var(--color-primary)"></span></button>
        <div class="flex items-center gap-3">
          <div class="grid h-9 w-9 place-items-center rounded-full text-xs font-bold" style="background:#31544a">JD</div>
          <div class="hide-mobile">
            <p class="text-xs font-semibold">Jean Doe</p>
            <p class="text-[11px]" style="color:var(--color-muted)">Security lead</p>
          </div><a href="/" class="ml-2 text-xs font-semibold" style="color:var(--color-muted)">Exit</a>
        </div>
      </div>
    </div>
  </header>
  <div class="mx-auto flex max-w-[1500px]">
    <aside class="sidebar sticky top-[73px] h-[calc(100vh-73px)] w-60 shrink-0 border-r px-4 py-7" style="border-color:var(--color-line)">
      <p class="mb-3 px-3 text-[10px] font-bold uppercase tracking-[.18em]" style="color:#61756e">Workspace</p>
      <nav class="space-y-1"><a href="/console" class="navitem active flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-semibold"><span>⌂</span> Overview</a><a href="#assets" class="navitem flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium"><span>◉</span> Asset inventory</a><a href="#observations" class="navitem flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium"><span>△</span> Observations <span class="ml-auto rounded-md px-2 py-0.5 text-[10px]" style="background:rgba(244,191,117,.12);color:var(--color-warning)">6</span></a><a href="#activity" class="navitem flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium"><span>↻</span> Sync activity</a></nav>
      <p class="mb-3 mt-9 px-3 text-[10px] font-bold uppercase tracking-[.18em]" style="color:#61756e">Administration</p>
      <nav class="space-y-1"><a href="#vault" class="navitem flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium"><span>▣</span> Secure records</a><a href="#settings" class="navitem flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium"><span>⚙</span> Settings</a></nav>
      <div class="absolute bottom-6 left-4 right-4 rounded-xl p-4" style="background:rgba(72,224,189,.06);border:1px solid rgba(72,224,189,.14)">
        <div class="flex items-center gap-2 text-xs font-semibold"><span class="h-2 w-2 rounded-full" style="background:var(--color-primary)"></span> All systems operational</div>
        <p class="mt-2 text-[11px]" style="color:var(--color-muted)">Last checked just now</p>
      </div>
    </aside>
    <main class="main-content min-w-0 flex-1 px-6 py-9 lg:px-10">
      <div class="mb-8 flex flex-col justify-between gap-5 sm:flex-row sm:items-end">
        <div>
          <p class="mb-2 text-sm" style="color:var(--color-muted)">Tuesday, 14 October 2025</p>
          <h1 class="text-3xl font-semibold tracking-tight lg:text-4xl">Good morning, Jean <span aria-hidden="true">✦</span></h1>
          <p class="mt-2 text-sm" style="color:var(--color-muted)">Here’s your security posture at a glance.</p>
        </div>
        <div class="flex gap-3"><button class="rounded-xl px-4 py-2.5 text-sm font-semibold" style="border:1px solid var(--color-line);color:var(--color-text)">Last 24 hours⌄</button><button class="rounded-xl px-4 py-2.5 text-sm font-bold" style="background:var(--color-primary);color:var(--color-primary-contrast)">＋ Add source</button></div>
      </div>
      <div class="mb-6 grid gap-4 sm:grid-cols-2 xl:grid-cols-4">
        <article class="panel p-5">
          <div class="flex items-start justify-between"><span class="text-sm" style="color:var(--color-muted)">Monitored assets</span><span class="rounded-lg px-2 py-1 text-xs" style="background:rgba(72,224,189,.1);color:var(--color-primary)">◉</span></div>
          <div class="mt-4 flex items-end justify-between"><strong class="text-3xl font-semibold">248</strong><span class="text-xs font-semibold" style="color:var(--color-primary)">↗ 5.1%</span></div>
          <p class="mt-2 text-xs" style="color:var(--color-muted)">Compared to last month</p>
        </article>
        <article class="panel p-5">
          <div class="flex items-start justify-between"><span class="text-sm" style="color:var(--color-muted)">Open observations</span><span class="rounded-lg px-2 py-1 text-xs" style="background:rgba(244,191,117,.1);color:var(--color-warning)">△</span></div>
          <div class="mt-4 flex items-end justify-between"><strong class="text-3xl font-semibold">06</strong><span class="text-xs font-semibold" style="color:var(--color-warning)">2 elevated</span></div>
          <p class="mt-2 text-xs" style="color:var(--color-muted)">2 assigned · 4 to review</p>
        </article>
        <article class="panel p-5">
          <div class="flex items-start justify-between"><span class="text-sm" style="color:var(--color-muted)">Sources connected</span><span class="rounded-lg px-2 py-1 text-xs" style="background:rgba(131,157,255,.1);color:#9aafff">↻</span></div>
          <div class="mt-4 flex items-end justify-between"><strong class="text-3xl font-semibold">12<span class="text-lg" style="color:var(--color-muted)">/12</span></strong><span class="text-xs font-semibold" style="color:var(--color-primary)">In sync</span></div>
          <p class="mt-2 text-xs" style="color:var(--color-muted)">Latest sync 4 minutes ago</p>
        </article>
        <article class="panel p-5">
          <div class="flex items-start justify-between"><span class="text-sm" style="color:var(--color-muted)">Posture score</span><span class="rounded-lg px-2 py-1 text-xs" style="background:rgba(72,224,189,.1);color:var(--color-primary)">✳</span></div>
          <div class="mt-4 flex items-end justify-between"><strong class="text-3xl font-semibold">92<span class="text-lg" style="color:var(--color-muted)">/100</span></strong><span class="text-xs font-semibold" style="color:var(--color-primary)">Good</span></div>
          <p class="mt-2 text-xs" style="color:var(--color-muted)">↑ 3 points this quarter</p>
        </article>
      </div>
      <div class="mb-6 grid gap-4 xl:grid-cols-[1.45fr_.85fr]">
        <section class="panel p-5 lg:p-6">
          <div class="mb-6 flex items-start justify-between">
            <div>
              <h2 class="text-base font-bold">Network health</h2>
              <p class="mt-1 text-xs" style="color:var(--color-muted)">Availability across monitored locations</p>
            </div><button class="rounded-lg px-3 py-2 text-xs" style="border:1px solid var(--color-line);color:var(--color-muted)">This week⌄</button>
          </div>
          <div class="mb-4 flex items-baseline gap-3"><strong class="text-3xl font-semibold">99.94%</strong><span class="text-xs font-semibold" style="color:var(--color-primary)">+0.08% <span style="color:var(--color-muted)">vs prior week</span></span></div>
          <div class="relative h-48">
            <div class="absolute inset-0 flex flex-col justify-between">
              <div class="flex items-center gap-3"><span class="w-8 text-[10px]" style="color:var(--color-muted)">100</span>
                <div class="flex-1 border-t" style="border-color:var(--color-line)"></div>
              </div>
              <div class="flex items-center gap-3"><span class="w-8 text-[10px]" style="color:var(--color-muted)">99.5</span>
                <div class="flex-1 border-t" style="border-color:var(--color-line)"></div>
              </div>
              <div class="flex items-center gap-3"><span class="w-8 text-[10px]" style="color:var(--color-muted)">99.0</span>
                <div class="flex-1 border-t" style="border-color:var(--color-line)"></div>
              </div>
              <div class="flex items-center gap-3"><span class="w-8 text-[10px]" style="color:var(--color-muted)">98.5</span>
                <div class="flex-1 border-t" style="border-color:var(--color-line)"></div>
              </div>
            </div><svg class="absolute bottom-0 left-10 right-0 h-full w-[calc(100%-40px)]" viewBox="0 0 640 180" preserveAspectRatio="none">
              <defs>
                <linearGradient id="fill" x1="0" x2="0" y1="0" y2="1">
                  <stop offset="0" stop-color="#48e0bd" stop-opacity=".2" />
                  <stop offset="1" stop-color="#48e0bd" stop-opacity="0" />
                </linearGradient>
              </defs>
              <path d="M0 48 C35 42 42 65 80 57 S122 48 156 56 S202 37 235 44 S280 61 316 49 S362 51 397 37 S442 51 478 43 S515 31 550 39 S603 25 640 30 V180 H0Z" fill="url(#fill)" />
              <path d="M0 48 C35 42 42 65 80 57 S122 48 156 56 S202 37 235 44 S280 61 316 49 S362 51 397 37 S442 51 478 43 S515 31 550 39 S603 25 640 30" fill="none" stroke="#48e0bd" stroke-width="2.5" />
            </svg>
          </div>
          <div class="ml-10 mt-3 flex justify-between text-[10px]" style="color:var(--color-muted)"><span>Mon</span><span>Tue</span><span>Wed</span><span>Thu</span><span>Fri</span><span>Sat</span><span>Sun</span></div>
        </section>
        <section class="panel p-5 lg:p-6">
          <div class="flex items-start justify-between">
            <div>
              <h2 class="text-base font-bold">Observation breakdown</h2>
              <p class="mt-1 text-xs" style="color:var(--color-muted)">Needs a human review</p>
            </div><a href="#observations" class="text-xs font-semibold" style="color:var(--color-primary)">View all →</a>
          </div>
          <div class="my-6 flex items-center gap-6">
            <div class="relative grid h-32 w-32 shrink-0 place-items-center rounded-full" style="background:conic-gradient(var(--color-warning) 0deg 122deg, #ed8585 122deg 185deg, #3d554c 185deg 360deg)">
              <div class="grid h-[94px] w-[94px] place-items-center rounded-full text-center" style="background:var(--color-surface)">
                <div><strong class="text-2xl">06</strong>
                  <p class="text-[10px]" style="color:var(--color-muted)">total</p>
                </div>
              </div>
            </div>
            <div class="space-y-3 text-xs">
              <p class="flex items-center gap-2"><i class="h-2 w-2 rounded-full" style="background:var(--color-danger)"></i><span style="color:var(--color-muted)">Elevated</span><strong class="ml-auto">2</strong></p>
              <p class="flex items-center gap-2"><i class="h-2 w-2 rounded-full" style="background:var(--color-warning)"></i><span style="color:var(--color-muted)">Review</span><strong class="ml-auto">3</strong></p>
              <p class="flex items-center gap-2"><i class="h-2 w-2 rounded-full" style="background:#3d554c"></i><span style="color:var(--color-muted)">Informational</span><strong class="ml-auto">1</strong></p>
            </div>
          </div>
          <div class="rounded-xl px-3 py-3 text-xs" style="background:rgba(244,191,117,.07);color:var(--color-muted)">Two observations are waiting for an owner.</div>
        </section>
      </div>
      <section class="panel overflow-hidden" id="observations">
        <div class="flex flex-col justify-between gap-4 border-b px-5 py-5 sm:flex-row sm:items-center lg:px-6" style="border-color:var(--color-line)">
          <div>
            <h2 class="text-base font-bold">Recent observations</h2>
            <p class="mt-1 text-xs" style="color:var(--color-muted)">A short list of items worth your attention</p>
          </div><a href="#observations" class="text-xs font-semibold" style="color:var(--color-primary)">Open observation queue →</a>
        </div>
        <div class="overflow-x-auto">
          <table class="w-full min-w-[700px] text-left">
            <thead>
              <tr class="text-[10px] uppercase tracking-wider" style="color:#71867e;background:rgba(255,255,255,.018)">
                <th class="px-6 py-3 font-semibold">Observation</th>
                <th class="px-4 py-3 font-semibold">Location</th>
                <th class="px-4 py-3 font-semibold">Priority</th>
                <th class="px-4 py-3 font-semibold">Owner</th>
                <th class="px-4 py-3 font-semibold">Updated</th>
                <th class="px-6 py-3"></th>
              </tr>
            </thead>
            <tbody class="text-xs">
              <tr class="border-t" style="border-color:var(--color-line)">
                <td class="px-6 py-4">
                  <div class="font-semibold">Device awaiting verification</div>
                  <div class="mt-1" style="color:var(--color-muted)">New endpoint seen on office network</div>
                </td>
                <td class="px-4 py-4" style="color:var(--color-muted)">North office</td>
                <td class="px-4 py-4"><span class="rounded-full px-2.5 py-1 font-semibold" style="background:rgba(244,191,117,.1);color:var(--color-warning)">Review</span></td>
                <td class="px-4 py-4" style="color:var(--color-muted)">Unassigned</td>
                <td class="px-4 py-4" style="color:var(--color-muted)">8 min ago</td>
                <td class="px-6 py-4" style="color:var(--color-muted)">···</td>
              </tr>
              <tr class="border-t" style="border-color:var(--color-line)">
                <td class="px-6 py-4">
                  <div class="font-semibold">Access review due soon</div>
                  <div class="mt-1" style="color:var(--color-muted)">Quarterly review for shared workspace</div>
                </td>
                <td class="px-4 py-4" style="color:var(--color-muted)">Cloud workspace</td>
                <td class="px-4 py-4"><span class="rounded-full px-2.5 py-1 font-semibold" style="background:rgba(242,120,120,.1);color:var(--color-danger)">Elevated</span></td>
                <td class="px-4 py-4" style="color:var(--color-muted)">John Doe</td>
                <td class="px-4 py-4" style="color:var(--color-muted)">42 min ago</td>
                <td class="px-6 py-4" style="color:var(--color-muted)">···</td>
              </tr>
              <tr class="border-t" style="border-color:var(--color-line)">
                <td class="px-6 py-4">
                  <div class="font-semibold">Source sync resumed</div>
                  <div class="mt-1" style="color:var(--color-muted)">Telemetry feed is reporting normally</div>
                </td>
                <td class="px-4 py-4" style="color:var(--color-muted)">West region</td>
                <td class="px-4 py-4"><span class="rounded-full px-2.5 py-1 font-semibold" style="background:rgba(72,224,189,.1);color:var(--color-primary)">Resolved</span></td>
                <td class="px-4 py-4" style="color:var(--color-muted)">John Doe</td>
                <td class="px-4 py-4" style="color:var(--color-muted)">1 hr ago</td>
                <td class="px-6 py-4" style="color:var(--color-muted)">···</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>
      <footer class="mt-8 flex flex-col justify-between gap-3 pb-4 text-xs sm:flex-row" style="color:var(--color-muted)"><span>All times shown in your local time zone.</span><span>Privacy first · Activity is auditable · Human-reviewed decisions</span></footer>
    </main>
  </div>
</body>

</html>`);
----------------------------------------

:root{color-scheme:dark;--bg:#080c14;--surface:#0d131e;--surface-2:#101824;--border:#1b2635;--muted:#738197;--text:#e7edf6;--purple:#9a7bff;--cyan:#63cfe3;--green:#45d6a1;--amber:#f2b866}
*{box-sizing:border-box}
html{scroll-behavior:smooth}
body{margin:0;background:var(--bg);color:var(--text);font-family:'DM Sans',Inter,system-ui,-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;font-size:14px;min-width:320px}
a{color:inherit;text-decoration:none}
button{font:inherit}
.shell{min-height:100vh}
.sidebar{position:fixed;inset:0 auto 0 0;width:232px;background:#0a0f18;border-right:1px solid #18212d;padding:26px 15px 17px;display:flex;flex-direction:column;z-index:5}
.brand{display:flex;align-items:center;gap:11px;padding:0 9px 35px}
.brand-mark{width:37px;height:37px;border:1px solid #7764c7;border-radius:11px;display:grid;place-items:center;color:#f3efff;font-size:21px;font-weight:700;background:linear-gradient(145deg,#24203d,#121927);box-shadow:0 0 23px #9276ff22}
.brand-mark span{color:#ac98ff;font-size:12px;margin-left:1px}.brand-copy{display:grid;gap:2px}.brand-copy strong{font-size:16px;letter-spacing:2.1px}.brand-copy small{font:9px 'DM Mono',monospace;color:#76849a;letter-spacing:1.1px}
.nav-label{font:10px 'DM Mono',monospace;letter-spacing:1.2px;color:#657288;padding:0 11px 12px}
.sidebar nav{display:grid;gap:5px}.nav-item{height:41px;padding:0 11px;border-radius:7px;display:flex;align-items:center;gap:12px;color:#96a2b4;font-size:13px;transition:background .2s,color .2s}.nav-item>span{font-size:18px;width:17px;text-align:center;color:#7d8ba0}.nav-item:hover{background:#111b29;color:#e9eff8}.nav-item.active{color:#e6dcff;background:linear-gradient(90deg,#a187ff1c,#a187ff08);box-shadow:inset 2px 0 #a287ff}.nav-item.active>span{color:#ad96ff}.nav-count{margin-left:auto;font:10px 'DM Mono',monospace;border-radius:10px;background:#392b4d;color:#d6c8ff;padding:2px 7px}
.sidebar-bottom{margin-top:auto}.operator-card{display:flex;align-items:center;gap:10px;padding:11px 9px;border:1px solid #1b2735;border-radius:8px;background:#0d141e}.operator-icon{width:29px;height:29px;border:1px solid #30445a;background:#162333;border-radius:50%;display:grid;place-items:center;color:#65d8ad;font-size:12px}.operator-card>div:nth-child(2){display:grid;gap:4px}.operator-card strong{font-size:11px;font-weight:600}.operator-card small{font-size:10px;color:#8290a3}.online-dot{display:inline-block;width:6px;height:6px;border-radius:50%;background:#49d5a1;box-shadow:0 0 8px #49d5a188;margin-right:5px;vertical-align:1px}.more{margin-left:auto;color:#8090a1;letter-spacing:2px}.sidebar-foot{display:flex;justify-content:space-between;padding:16px 4px 0;color:#536176;font:9px 'DM Mono',monospace;letter-spacing:.8px}.sidebar-foot span{color:#69788d}
.main-content{margin-left:232px;padding:0 34px 24px;max-width:1800px}.topbar{height:62px;border-bottom:1px solid #17212e;display:flex;align-items:center;justify-content:space-between}.breadcrumb{font:10px 'DM Mono',monospace;letter-spacing:.85px;color:#8591a4}.breadcrumb span{padding:0 9px;color:#4b5a6d}.breadcrumb strong{color:#c5cedc;font-weight:400}.topbar-right{display:flex;align-items:center;gap:17px;color:#8290a3}.live-label{font:9px 'DM Mono',monospace;letter-spacing:.55px;color:#b5c5c5}.top-divider{height:19px;width:1px;background:#25303d}.clock{font:10px 'DM Mono',monospace;color:#8997a9}.avatar{border:1px solid #344154;color:#dcd4ff;background:#19172a;border-radius:50%;width:30px;height:30px;font:10px 'DM Mono',monospace}
.welcome{padding:31px 0 22px;display:flex;justify-content:space-between;align-items:flex-end;gap:20px}.eyebrow{display:flex;align-items:center;gap:8px;color:#a690ff;font:9px 'DM Mono',monospace;letter-spacing:1.35px}.eyebrow-line{display:block;height:1px;width:19px;background:#9b7cff}.welcome h1{font-size:28px;letter-spacing:-.9px;margin:8px 0 5px;font-weight:600}.welcome h1 span{color:#b6a3ff}.welcome p,.section-heading p,.panel-heading p{margin:0;color:#8491a4;font-size:12px}.button{cursor:pointer;border-radius:6px;padding:9px 12px;white-space:nowrap}.button-secondary{color:#bdc7d5;background:#101722;border:1px solid #273344;font-size:11px;transition:.2s}.button-secondary:hover{border-color:#806fd1;background:#171c2c}.refresh-icon{font-size:15px;color:#b8a4ff;margin-right:5px;display:inline-block}.button.is-refreshing .refresh-icon{animation:spin .7s linear infinite}@keyframes spin{to{transform:rotate(360deg)}}
.status-banner{position:relative;overflow:hidden;min-height:99px;border-radius:9px;border:1px solid #234035;background:linear-gradient(100deg,#10231f 0%,#101d20 47%,#101722 100%);padding:18px 20px;display:flex;align-items:center;gap:14px}.status-emblem{width:38px;height:38px;flex:0 0 38px;display:grid;place-items:center;border-radius:50%;border:1px solid #3b8e70;background:#173b31;color:#6be0ad;font-size:20px;box-shadow:0 0 22px #41d39a18}.status-copy{display:grid;gap:4px;min-width:245px}.status-kicker,.banner-meta>span{color:#85a99b;font:9px 'DM Mono',monospace;letter-spacing:.8px}.status-copy>strong{font-size:16px;font-weight:600}.status-copy>small{font-size:11px;color:#93a79f}.status-pill{margin-left:7px;vertical-align:2px;border:1px solid #287a5c;background:#163629;border-radius:20px;padding:3px 7px;color:#62d8a2;font:8px 'DM Mono',monospace;letter-spacing:.4px}.banner-meta{margin-left:auto;display:grid;gap:7px;position:relative;z-index:1}.banner-meta strong{font:12px 'DM Mono',monospace;color:#d0dbd4}.banner-spark{height:36px;display:flex;align-items:center;gap:4px;margin:0 4px 0 22px;opacity:.55}.banner-spark span{width:3px;border-radius:3px;background:#46ca95;height:var(--h,40%)}.banner-spark span:nth-child(3n){--h:80%}.banner-spark span:nth-child(3n+1){--h:55%}.banner-spark span:nth-child(4n){--h:100%}.banner-spark span:nth-child(5n){--h:29%}
.metric-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px;margin-top:15px}.metric-card,.system-card,.panel{border:1px solid var(--border);background:linear-gradient(145deg,#0e1520,#0c121b);border-radius:8px}.metric-card{padding:14px 15px 11px;min-width:0}.metric-head{display:flex;align-items:center;justify-content:space-between;color:#8c99aa;font:9px 'DM Mono',monospace;letter-spacing:.45px}.metric-icon{width:23px;height:23px;display:grid;place-items:center;border-radius:6px;font-size:15px}.purple{color:#b69dff;background:#312951}.amber{color:#f0bc69;background:#3a2b1a}.cyan{color:#70d5e6;background:#16343b}.green{color:#62d6a6;background:#15372d}.metric-value{font:500 26px 'DM Mono',monospace;letter-spacing:-1px;color:#e6edf7;margin:9px 0 8px}.value-unit{font-size:12px;color:#a0adbd;letter-spacing:0}.metric-foot{border-top:1px solid #1a2431;padding-top:9px;display:flex;align-items:center;gap:7px;white-space:nowrap;color:#728096;font-size:9px;position:relative}.trend{font:9px 'DM Mono',monospace}.positive{color:#53d3a0}.neutral{color:#edbd70}.metric-foot svg{width:52px;height:20px;margin-left:auto;overflow:visible}.metric-foot svg path{fill:none;stroke:#a187ff;stroke-width:1.7}.metric-foot svg.amber-line path{stroke:#eeb55e}.metric-foot svg.cyan-line path{stroke:#60cde0}.metric-foot svg.green-line path{stroke:#4fd5a0}
.section-heading{margin:26px 0 12px;display:flex;justify-content:space-between;align-items:flex-end}.section-heading h2,.panel-heading h2{font-size:15px;margin:0 0 4px;font-weight:600;letter-spacing:-.2px}.section-heading p,.panel-heading p{font-size:11px}.text-link{color:#a895ff;font-size:10px}.text-link span{padding-left:4px}.text-link:hover{color:#d1c7ff}.system-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px}.system-card{padding:13px 14px 11px;min-width:0;transition:border-color .2s,transform .2s}.system-card:hover{border-color:#39445c;transform:translateY(-2px)}.system-top{display:flex;justify-content:space-between;align-items:center}.system-icon{width:29px;height:29px;border-radius:7px;display:grid;place-items:center;font-size:17px}.icon-violet{background:#28203e;color:#b49cff}.icon-blue{background:#192744;color:#83adff}.icon-cyan{background:#16333a;color:#68d4e3}.icon-green{background:#17352c;color:#64d4a3}.system-status{display:flex;align-items:center;gap:5px;color:#6acba2;font:8px 'DM Mono',monospace;letter-spacing:.25px}.system-status i{width:5px;height:5px;background:#4bd09a;border-radius:50%;box-shadow:0 0 7px #4bd09a77}.system-card h3{font-size:12px;margin:11px 0 4px;font-weight:600}.system-card>p{height:28px;margin:0;color:#8491a4;font-size:10px;line-height:1.45}.system-bottom{border-top:1px solid #1b2633;margin-top:9px;padding-top:8px;display:flex;justify-content:space-between;align-items:center}.system-bottom>span{font:8px 'DM Mono',monospace;color:#657489;letter-spacing:.3px}.system-bottom strong{font-size:9px;font-weight:500;color:#c1ccda}.mini-check{font-style:normal;color:#58d5a0;margin-left:3px}
.lower-grid{display:grid;grid-template-columns:1.15fr .85fr;gap:12px;margin-top:17px}.panel{padding:15px 15px 11px;min-width:0}.panel-heading{display:flex;align-items:flex-start;justify-content:space-between;gap:12px}.panel-heading h2{font-size:13px}.panel-heading p{font-size:10px}.select-display{border:1px solid #253142;border-radius:4px;padding:5px 7px;color:#95a2b4;font:8px 'DM Mono',monospace;white-space:nowrap}.chart-legend{display:flex;gap:17px;margin-top:16px;color:#8491a4;font-size:9px}.legend-dot{width:6px;height:6px;display:inline-block;border-radius:50%;margin-right:5px}.purple-dot{background:#a58aff}.cyan-dot{background:#64d1df}.chart{display:flex;height:149px;margin-top:9px}.chart-y{width:26px;display:flex;flex-direction:column;justify-content:space-between;padding:0 0 18px;color:#627187;font:8px 'DM Mono',monospace}.chart-area{position:relative;flex:1;min-width:0}.grid-lines{position:absolute;inset:0 0 19px;display:flex;flex-direction:column;justify-content:space-between}.grid-lines i{border-top:1px dashed #222d3a}.chart-area svg{position:absolute;inset:0 0 19px;width:100%;height:calc(100% - 19px);overflow:visible}.area-path{fill:url(#fillPurple)}.chart-line{fill:none;stroke-width:2;vector-effect:non-scaling-stroke}.detected-line{stroke:#a78bfa}.blocked-line{stroke:#60cddb;stroke-width:1.6}.chart-x{position:absolute;bottom:0;left:0;right:0;display:flex;justify-content:space-between;color:#66758a;font:8px 'DM Mono',monospace}.activity-panel{padding-bottom:4px}.activity-list{margin-top:10px}.activity-item{display:flex;align-items:center;gap:9px;padding:10px 0;border-top:1px solid #1a2430;min-width:0}.activity-mark{flex:0 0 25px;height:25px;border-radius:6px;display:grid;place-items:center;font-size:13px}.blocked{color:#f0a874;background:#38251f}.scan{color:#a995ff;background:#28213d}.policy{color:#5bd2a0;background:#17342b}.update{color:#67cce0;background:#17313a}.activity-detail{min-width:0;display:grid;gap:4px}.activity-detail strong{font-size:9px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.activity-detail small{color:#7a889c;font-size:8px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.activity-item time{margin-left:auto;align-self:flex-start;padding-top:2px;color:#728096;font:8px 'DM Mono',monospace;white-space:nowrap}.footer{display:flex;justify-content:space-between;gap:12px;padding:18px 1px 0;color:#566477;font:8px 'DM Mono',monospace;letter-spacing:.45px}.footer i{font-style:normal;color:#896fff;padding:0 4px}.footer span:last-child{letter-spacing:0;color:#566477}
.toast{position:fixed;right:25px;bottom:22px;padding:10px 15px;border:1px solid #315545;border-radius:7px;background:#10251e;color:#a7ebce;font-size:11px;opacity:0;transform:translateY(8px);pointer-events:none;transition:.22s;z-index:10}.toast.show{opacity:1;transform:translateY(0)}
@media(max-width:1100px){.main-content{padding-left:24px;padding-right:24px}.sidebar{width:205px}.main-content{margin-left:205px}.metric-grid,.system-grid{grid-template-columns:repeat(2,minmax(0,1fr))}.banner-spark{display:none}.lower-grid{grid-template-columns:1fr}.activity-item{padding:9px 0}}
@media(max-width:700px){.sidebar{position:relative;width:100%;height:auto;padding:13px 15px;border-right:0;border-bottom:1px solid #18212d}.brand{padding:0}.sidebar .nav-label,.sidebar-bottom{display:none}.sidebar nav{display:flex;gap:4px;margin-top:13px;overflow-x:auto}.nav-item{height:35px;padding:0 9px;white-space:nowrap;font-size:11px}.nav-item>span{font-size:15px}.nav-count{padding:1px 5px}.main-content{margin:0;padding:0 15px 20px}.topbar{height:48px}.breadcrumb{font-size:8px}.topbar-right{gap:9px}.live-label{font-size:8px}.clock{font-size:8px}.top-divider{height:15px}.avatar{width:27px;height:27px}.welcome{padding-top:24px;align-items:flex-start}.welcome h1{font-size:23px}.welcome p{max-width:350px;font-size:11px;line-height:1.5}.button-secondary{font-size:0;padding:8px 10px}.refresh-icon{font-size:17px;margin:0}.status-banner{padding:14px 12px;gap:10px;flex-wrap:wrap}.status-emblem{width:33px;height:33px;flex-basis:33px}.status-copy{min-width:0;flex:1}.status-copy>small{font-size:10px}.banner-meta{margin:5px 0 0 43px;min-width:100px}.banner-meta:last-of-type{margin-left:auto}.metric-grid{gap:8px}.metric-card{padding:12px 10px 9px}.metric-head{font-size:8px}.metric-value{font-size:23px}.metric-foot{font-size:8px;gap:5px}.metric-foot svg{width:30px}.section-heading{margin-top:22px}.system-grid{gap:8px}.system-card{padding:11px 10px 9px}.system-status{font-size:7px}.lower-grid{margin-top:13px}.footer{flex-direction:column}.panel{padding:13px 11px 9px}}
@media(max-width:400px){.topbar-right{gap:7px}.live-label{font-size:7px;letter-spacing:0}.clock{font-size:7px}.welcome{gap:8px}.welcome h1{font-size:21px}.welcome p{font-size:10px}.metric-foot svg{display:none}.metric-head{font-size:7px}.banner-meta{margin-left:42px}.system-status{letter-spacing:0}.system-card>p{font-size:9px}}
@media(prefers-reduced-motion:reduce){*,*::before,*::after{scroll-behavior:auto!important;animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important}}
