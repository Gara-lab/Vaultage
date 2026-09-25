---
title: "Storage_interface_templates — Decisions"
tags: [storage_interface_templates, decisions]
created: 2026-09-18
type: decisions
---

- **2026-09-18** — On the V2 seed mockup's data tables, a status-dot + number pairing (`.status-cell`) uses `column-gap` for dot-to-number spacing but must NOT use the parent `<td>`'s own `text-align` to position the dot — variable-width content right-aligned in a `<td>` shifts the dot's left edge per row. Fix pattern: keep the `.status-cell` box left-aligned within its `<td>` (a dedicated `status-col` class forcing `text-align: left` on that cell) so the dot stays pinned, while spacing inside the box is controlled separately via `column-gap`/`auto` grid columns.
