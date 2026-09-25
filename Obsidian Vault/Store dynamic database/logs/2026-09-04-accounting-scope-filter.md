---
title: "Store dynamic database — Accounting scope filter (FR15) + color fix"
tags: [store-dynamic-database, session-log]
created: 2026-09-04
type: session-log
status: imported
---

# Accounting scope filter (FR15) + color fix

## Summary
Planned and implemented FR15: a new Active/Deleted/All scope filter on the Accounting
view, letting the user distinguish sale figures coming from currently-active items vs.
soft-deleted ones (or see both combined, the default). Added `Calc.filterSaleEventsByItemScope`
(js/calc.js, pure, non-mutating, dynamic reclassification per CT-11) with 5 new test
checks (AC25-AC29), and a new Scope segmented-button row in js/view-accounting.js above
the existing granularity picker. Ran the full CLAUDE.md Completion Loop: enforcer caught
missing test coverage (fixed), planner FINAL REVIEW caught two stale doc references to
the pre-2026-09-02 Delete-button treatment (fixed with SUPERSEDED markers), and
goal-evaluator initially blocked on missing log evidence (fixed) before returning ok.
After shipping, the user reported in-browser that selecting a scope option removed the
button's border but never turned it green. Root-caused to the theme's `--s` (secondary)
token being a pale near-white nearly identical to the card background — fixed by
switching the active-state class from `btn-secondary` to `btn-primary`, verified by a
second enforcer + goal-evaluator pass.

## Decisions
- Scope filter defaults to "All" so it never silently changes existing totals for
  existing users (FR15 requirement).
- Scope classification is dynamic — read from `itemsById` at render time, not a
  sale-time snapshot — so deleting an item today retroactively reclassifies its past
  sales in every past period (CT-11).
- Reuses the existing granularity-picker's `join`/`btn-outline`/segmented-button pattern
  rather than a new control style; distinctness from the granularity picker comes from
  the "Scope" caption label and row position, not a different color.
- Active-state color is `btn-primary` (`#1F6F4F`), not `btn-secondary` (`#E7EEE4`) —
  the latter is visually indistinguishable from the `--b2` card background even though
  it passes AA text-contrast. See decisions.md for the durable lesson.
- View Items changes are explicitly deferred by the user until later; not started this
  session.

## Open items
- View Items changes — deferred, waiting on the user to bring it up again.

## Files touched
- js/calc.js — added `filterSaleEventsByItemScope`
- js/calc.test.js — added AC25-AC29
- js/view-accounting.js — added Scope picker (buildSkeleton, updateContent), scope-aware
  rollup call, color fix (`btn-secondary` → `btn-primary`)
- architecture.md — S1/S2 task plan, 2026-09-04 fix note
- ux.md — Accounting scope filter decision section (+ revised/superseded color decision)
- contracts.md — CT-11
- data-model.md, workflows.md, requirements.md, testing.md — FR15 spec updates;
  workflows.md W6 step 1 and testing.md AC23 SUPERSEDED markers for stale Delete-button
  references
- AGENT_LOG.md — full task/decision log for this session's work
