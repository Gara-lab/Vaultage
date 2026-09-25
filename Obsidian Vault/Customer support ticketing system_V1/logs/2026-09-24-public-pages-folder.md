---
title: "Customer support ticketing system_V1 — group public pages into public/ folder"
tags: [customer-support-ticketing-system-v1, session-log]
created: 2026-09-24
type: session-log
status: imported
---

# Group public pages into public/ folder

## Summary
User initially asked to merge `status.html` and `kb.html` into a single `index.html` (one-file site). Before implementing, flagged that this would force an SPA-style show/hide-section pattern, which introduces a real bug class (wrong section visible) that the current multi-page structure doesn't have — recommended against it. User agreed and instead asked to group the non-index public pages into their own folder as a better long-term habit. Implemented Task 24: created `public/`, moved `status.html` and `kb.html` into it, and updated every relative path/link sitewide (both moved pages' own css/js/data/nav paths, `index.html`'s nav + ticket-confirmation link, and the three department login pages' Statut/FAQ nav links). Only one line of actual logic changed (`js/ticket-form.js`'s confirmation-link href, since the target file moved) — no other content or behavior changed in any page. Updated `ARCHITECTURE.md` and this project's `CLAUDE.md` to reflect the new page-location convention, logged as Task 24 in `AGENT_LOG.md`, verified live via Playwright (10/10 checks passed, zero console/page errors), and passed the Completion Loop with `goal-evaluator: ok`.

## Decisions
- Rejected merging `status.html`/`kb.html`/`index.html` into a single file — MPA (separate files) is safer than SPA-style section toggling for this site, given the user's actual concern was avoiding link/visibility bugs, not file count.
- Instead adopted a `public/` folder convention: `index.html` stays at the project root (served as `/` by any static host), and all other public-facing pages (currently `status.html`, `kb.html`) live under `public/` — established now, before more public pages exist, specifically to avoid loose files piling up at the root later.

## Open items
None — Task 24 is complete, documented, and evaluator-approved.

## Files touched
- `public/status.html`, `public/kb.html` (moved from project root, paths updated, content untouched)
- `index.html` (nav links + confirmation link updated to `public/...`)
- `admin/login.html`, `hr/login.html`, `it/login.html` (nav Statut/FAQ links updated to `../public/...`)
- `js/ticket-form.js` (one-line confirmation-link href update)
- `ARCHITECTURE.md`, `CLAUDE.md`, `AGENT_LOG.md` (docs/log updated)
