---
title: "Library templates — Chip alignment fix and site-wide background rework"
tags: [library-templates, session-log]
created: 2026-09-09
type: session-log
status: imported
---

# Chip alignment fix and site-wide background rework

## Summary
Continued building the static template-library site (gallery + precision-dark + material-design-3 demo pages). Fixed a filter-chip alignment bug on the material-design-3 page (long label inside a full-pill shape was wrapping and misaligned — shortened the text and stopped the chip stretching in its grid cell). Then reworked the site's background handling after two rejected attempts: landed on one plain light background directly on `body` for every page, no wrapping block/frame anywhere, with precision-dark's own demo panels (swatches, type/style/block examples) keeping small scoped dark backing so they still show the template's real colours. Along the way, caught and fixed a related bug where translucent hover/active tints were compositing against the new light page instead of their dark surface. Verified complete via the mandatory `goal-evaluator` check (VERDICT: ok).

## Decisions
See `decisions.md` for the durable ones (page-background architecture, `--page-*` vs `--color-*` split, tint-layering pattern, composition-guide structure). Nothing new added this session beyond what's already logged there.

## Open items
- Git/GitHub/Pages deployment remains explicitly deferred by the user — not to be raised again.
- material-design-3's `generate_palette.py` remains available but unused (real reference already covered every colour role).
- No other open bugs or unresolved feedback as of this session's end.

## Files touched
- `templates/material-design-3/index.html`, `templates/material-design-3/style.css` (chip fix)
- `assets/tokens.css`, `assets/site.css` (page-chrome/`--page-*` variables, tint-layering fix)
- `templates/precision-dark/style.css`, `templates/precision-dark/index.html` (background rework, demo-panel scoped dark backing)
- `AGENT_LOG.md`, `CODE_MAP.md` (progress, decisions, and gotcha entries)
- Removed: `assets/shell.css` (created then fully reverted)
