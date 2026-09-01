# status

Self-owned uptime monitoring for the XOLBY / Prosper Flow production surfaces.
Born from INCIDENT-2026-07-30 in the focus repo ("No uptime monitoring — the
outage was discovered only because a routine CLI call returned 504 hours
later") and the 2026-08-28 Netlify credit pause that took every client site
down silently.

**How it works:** [uptime.yml](.github/workflows/uptime.yml) probes each site
every 5 minutes from GitHub's infrastructure — deliberately outside Fly,
Netlify, and any personal machine, because a system cannot be trusted to
report its own death.

**When something is down:**
1. The run fails → GitHub emails the owner (survives everything else being down).
2. An `incident` issue opens for the site and **closes itself on recovery** —
   the issue's open duration is the outage duration, so the issues tab is the
   incident log.
3. Best-effort, an urgent task is filed into Focus (Role Coverage → Alerts) so
   the dashboard and the morning autopilot see it. Skipped gracefully when
   Focus itself is the casualty.

**Monitored:** Focus API (Fly), Focus app (Netlify), American Muffler &
Towing, iLights Modern, XOLBY, Truth In Beauty, Rachelle's Cleaning Service,
Lena's Wreath Decor — the list lives at the top of the
workflow; adding a site is one line.

This repo is public on purpose: it contains only public URLs, and public
repos get unlimited free Actions minutes — a private cron this frequent would
burn ~4,000 billed minutes a month, recreating the billing exhaustion that
caused one of the outages it exists to catch.
