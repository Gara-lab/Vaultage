---
title: "V2 — Decisions"
tags: [v2, decisions]
created: 2026-09-10
type: decision-log
---

- **2026-09-10** — Serve `seed/` over http (npx live-server for dev, a throwaway Python `http.server` inside `test_mockup.py` for the automated check) instead of opening `index.html` via `file://`, because native ES modules are blocked under `file://` by browser CORS rules.
- **2026-09-10** — Stocktake counted quantity can never exceed current system stock; a stocktake only confirms or reduces stock (no surplus/new-lot branch), since a surplus with no real purchase behind it shouldn't become sellable inventory.
- **2026-09-11** — Dead-stock threshold fixed at 30 days, same fixed-constant pattern as the 14-day low-stock reorder horizon; not configurable, revisit only if a real tuning need arises.
- **2026-09-11** — Reports CSV export is scoped to the visible table only (no library); a separate "Export all (3 files)" / "Export all (1 file)" pair of buttons exists for exporting all three report tables at once, kept as two distinct, clearly-labeled buttons rather than one to avoid ambiguity between the two behaviors.
- **2026-09-11** — For the rest of this project, implementation work is delegated to subagents/background workflows rather than done directly in the main thread, even for small-looking tasks — protects the long session's context window and reduces hallucination risk over the project's full lifetime.
- **2026-09-11** — The real, non-mockup MVP will be built as a separate future project (Node.js/Express, PostgreSQL, multi-tenant with one shared login per shop, self-serve signup, low-ops PaaS hosting), planned in `mvp-plan/` inside this project but not yet scaffolded or implemented — this mockup (`seed/`) stays frozen as the reference spec until that happens.

## Logs
- [[V2/logs/2026-09-10-stocktake-preview-badges|Stocktake preview badges]]
- [[V2/logs/2026-09-11-help-tab|Help tab]]
- [[V2/logs/2026-09-11-mvp-plan|Real mvp planning]]
- [[V2/logs/2026-09-11-reports-and-ux-refinements|Reports and ux refinements]]
