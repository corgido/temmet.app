# temmet

Live meeting cost meter. No account, no server, no data leaves your browser.

**Live app:** [temmet.app](https://temmet.app)
**Docs:** [temmet.app/learn](https://temmet.app/learn/)

![temmet setup screen](/images/temmet_sample_1.png)

![temmet live session](/images/temmet_sample_2.png)

## What it does

You add participants, set hourly rates, press start, and the running total climbs in real time. Meetings have a real cost that nobody sees. temmet makes it visible — to the room, in real time — so teams can make better decisions about what deserves a meeting and what doesn't.

## What I built

A full-stack client-side application — React 18, TypeScript, Vite — with an offline-first architecture that stores everything in IndexedDB. No back-end server, no database, no API, no user accounts. The entire product runs in the browser.

A static documentation site at /learn — 19 pages of guides, glossary, and recipes generated at build time from Markdown. Zero JavaScript. Each page carries structured data (JSON-LD), Open Graph metadata, and a canonical URL.

## Scope

- 86 React components, 14 test suites (97 tests), ~5,700 words of documentation
- Simple mode (slider-based) and Advanced mode (per-participant roles, rates, templates)
- Live meter with pause/resume, keyboard shortcuts, crash-resilient session checkpoints
- Session history with search, sort, date filtering, comparison, and analytics charts
- Export to CSV, JSON, or PDF — full dataset or selection-only
- Reusable templates with save, load, edit, duplicate, and undo
- Theme support (light/dark/system), wake lock, currency as free-text

## Key decisions

| Decision | Why |
|---|---|
| No server | Zero infrastructure cost, zero attack surface for user data. The privacy claim is architectural, not policy. |
| IndexedDB over localStorage | Structured data — sessions carry nested participant arrays. Schema-versioned with migrations, validated on read. |
| Static HTML for /learn, not React routes | Zero bundle cost to the app, instant page loads, crawler-friendly without JS, independent deploy cadence. |
| Selection-aware export | Turns the app into a per-client invoice tool — pick the sessions, export the PDF. |
| Context-based state for session flow | Fixed a class of bugs where independent useState copies diverged across components. |
| CSP with no third-party origins | default-src 'self'. Combined with HSTS, X-Frame-Options DENY, and a Permissions-Policy denying camera/mic/geo/payment. |
| ErrorBoundary with data-reset escape hatch | If the app state corrupts, the user can recover without losing IndexedDB data. |
| Build-time llms.txt and sitemap | Documentation is discoverable by crawlers and LLMs without runtime JS. Duplicate-slug collisions hard-fail the build. |
