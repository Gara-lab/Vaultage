---
title: "V2 — Stocktake preview: confirmed/loss as colored badges"
tags: [v2, session-log]
created: 2026-09-10
type: session-log
status: imported
---

# Stocktake preview: confirmed/loss as colored badges

## Summary
Converted the Stocktake tab's live per-row preview text ("confirmed, no change" / "will record a loss of N") into colored badge/tag elements, reusing the app's existing `.badge` CSS component instead of inventing a new one. Added one new modifier class, `.badge.confirmed` (green), and reused the existing `.badge.loss` (red). The "exceeds current stock" case was left as plain red text since the user only asked about the confirmed/loss pair. A test assertion in `test_mockup.py` broke as a side effect (the badge's `text-transform: uppercase` changes what Playwright's `inner_text()` reports) and was fixed by adding `.lower()` to match the sibling assertions in the same test. Full Playwright suite passes; goal-evaluator returned VERDICT: ok.

## Decisions
None (see decisions.md for standing project decisions; nothing new this session).

## Open items
- Phase 1C: reports (top/slow movers, dead-stock list, CSV export) — approved, not started.
- Phase 1D UX refinements (one-tap sale qty default, quick purchase receive, search by name/category) — approved, not started.
- Data export/backup UI — `store.js`'s `exportBackup()` exists but has no exposed UI button yet.

## Out of scope for this MVP (not removed — candidates for a future version)
- Barcode/QR scanning (and the associated `Product.code` field).
- Multi-user support / permissions.

## Files touched
- `seed/index.html` — added `.badge.confirmed` CSS rule.
- `seed/js/stocktake.js` — `updatePreview()` now renders badges for the confirmed/loss cases.
- `seed/test_mockup.py` — fixed one assertion (`.lower()`) in `stocktake_live_preview_shows_consequence_before_saving`.
