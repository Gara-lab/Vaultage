---
title: "Storage interface — Decisions"
tags: [storage-interface, decisions]
created: 2026-09-09
type: decisions
---

# Decisions

- **2026-09-09** — Cost basis for margin/gain uses FIFO lot tracking (not weighted average): user wants per-lot cost precision, with lot history visible in the Product Detail UI.
- **2026-09-09** — Single storage location only, no location dimension anywhere in the app: business operates from one location.
- **2026-09-09** — Single user (the owner), no login/auth or multi-user roles in the mockup: only the owner uses the app.
- **2026-09-09** — Stock is reduced by two distinct event types — Sales (sale price captured, gain computed via FIFO cost) and Loss/Adjustment (shrinkage/damage/theft, no revenue) — kept as separate flows so losses aren't mistaken for revenue.
- **2026-09-09** — Mockup targets one responsive build (mobile + desktop) rather than separate mockups per platform.
- **2026-09-09** — Dashboard "stock value (at cost)" shows the opening balance as of the start of the selected period (Today/Week/Month), replaying the FIFO ledger back to that date — not a static "current" figure, so it reacts to the period toggle like revenue/margin/losses do.
- **2026-09-09** — Selling-price updates are entered as an optional field on the Record Purchase flow, not Record Sale: the brief ties price fluctuation to new purchases, and bundling it into the far higher-frequency Record Sale action would add friction to the busiest workflow for a time-pressed owner.

## Logs
- [[Storage interface/logs/2026-09-09-mockup-phase-complete|Mockup phase complete]]
