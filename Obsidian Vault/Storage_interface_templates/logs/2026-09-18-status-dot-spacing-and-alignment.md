---
title: "Storage_interface_templates — Status-dot spacing and alignment fixes"
tags: [storage_interface_templates, session-log]
created: 2026-09-18
type: session-log
status: imported
---

# Status-dot spacing and alignment fixes

## Summary
Iterated on the V2 seed mockup's Inventory/Stocktake/Purchase-history tables. Fixed missing column labels on the Purchase-history table on mobile (added `data-label` attributes), tightened the visual gap between status dots and their numbers in Inventory/Stocktake (root cause was leftover flex space from a `1fr` grid column, not the `column-gap` value itself), paired "Supplier" alongside "Unit cost" instead of forcing it onto its own row in the Purchase-history table, and then fixed a self-introduced regression where desktop status dots became misaligned across rows after the spacing fix (root cause: a variable-width `.status-cell` box was being positioned by the parent `<td>`'s `text-align: right`). Every fix was verified with Playwright screenshots at mobile and desktop viewports and independently confirmed by the `goal-evaluator` subagent before being reported done.

## Decisions
- See `decisions.md`: dot-alignment must be controlled by the `<td>`'s own `text-align` on a dedicated class, kept separate from internal dot-to-number spacing inside `.status-cell`.

## Open items
- None requested. Dormant, non-actioned notes from an earlier ponytail audit remain unqueued: extracting `wireIconPicker()` in product-form.js, extracting a shared `initPeriodSelector()` between dashboard.js/reports.js, deleting a stray `.pyc` in `seed/__pycache__/`, and a minor note that the Margin column needs internal horizontal scroll on tablet width (768px) in Inventory.

## Files touched
- `Storage_interface_templates/V2/seed/index.html` — `.status-cell` grid/spacing rules, new `.data-table td.status-col { text-align: left; }` rule, `.lots-table td:last-child { grid-column: auto; }` mobile override.
- `Storage_interface_templates/V2/seed/js/inventory.js` — added `status-col` class to Stock/Margin `<td>`s.
- `Storage_interface_templates/V2/seed/js/stocktake.js` — added `status-col` class to System-qty `<td>`.
- `Storage_interface_templates/V2/seed/js/product-detail.js` — added missing `data-label` attributes to Purchase-history table cells, added `lots-table` class to that table.
