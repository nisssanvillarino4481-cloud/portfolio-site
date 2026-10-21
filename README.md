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
