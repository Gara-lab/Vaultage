---
title: "Store dynamic database — Decisions"
tags: [store-dynamic-database, decisions]
created: 2026-09-03
type: decisions
---

# Decisions

- **2026-09-03** — Accounting view gets a Scope filter (Active / Deleted / All items, default All) so sale figures from soft-deleted items can be distinguished from currently-active items or combined — reuses the existing granularity-picker's segmented-button pattern rather than inventing a new control style.
- **2026-09-04** — Scope filter's active-state button color is `btn-primary` (the theme's real green, `#1F6F4F`), not `btn-secondary` — the theme's `--s` secondary token (`#E7EEE4`) is a pale near-white nearly identical to the card background, so a filled `btn-secondary` button did not read as "selected" even though it passed AA text-contrast checks. Lesson: AA text-contrast passing does not guarantee a fill color is perceptible against its surroundings — needs actual visual/in-browser check, not just a contrast-ratio calculation.
- **2026-09-04** — View Items changes are deferred (user's explicit request) — Accounting work took priority and is being finished first; do not start View Items work until the user brings it up again.
- **2026-09-04** — View Items changes are cancelled outright (superseded the deferral above) — the user said the change is no longer necessary; nothing was ever started there.
- **2026-09-04** — Zero comments allowed in `js/*.js`, permanently, no exceptions (not even JSDoc). Any non-obvious why/invariant/gotcha goes into `CODE_MAP.md` instead of a comment; a genuine product/business decision found hiding in what would have been a comment gets promoted into the applicable spec doc (ux.md, architecture.md decision log, etc.), never into `CODE_MAP.md`. Enforced via a CLAUDE.md rule plus a dedicated checklist item in `.claude/agents/enforcer.md` so it doesn't depend on the lead agent remembering. Root cause of the original regression: spec-doc content (from the project's `.md` files) was being duplicated into inline code comments, driving comment density to ~34% of the codebase.

## Logs
- [[Store dynamic database/logs/2026-09-04-accounting-scope-filter|Accounting scope filter]]
- [[Store dynamic database/logs/2026-09-04-comment-cleanup-code-map|Comment cleanup code map]]
