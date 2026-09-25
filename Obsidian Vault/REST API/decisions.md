---
title: "REST API — Decisions"
tags: [rest-api, decisions]
created: 2026-08-25
type: decision-log
status: imported
---

- **2026-08-25** — Backend stack = Python + FastAPI + Pydantic (user chose the Python route for Module 1; sets the stack for the whole project).
- **2026-08-25** — Adopt Pattern B (ARCHITECTURE.md + CONTRACTS.md) from the start, since the project is long-running with multiple future modules.
- **2026-08-25** — Enforce ports-and-adapters layering so `core/domain` and `core/services` never import third-party libraries directly (Pydantic, FastAPI) — only `adapters/` and `api/` do, so swapping libraries later doesn't ripple through the rest of the API.
- **2026-08-25** — Coding standard is atomic, KISS-style changes, with heavy use of Implementer/Enforcer subagents and the Workflow tool for independent sub-pieces to keep the lead agent's context low over the project's long lifetime.
- **2026-08-25** — Module 2 persistence = stdlib `sqlite3` with raw parameterized SQL (in-memory DB, seeded at startup), chosen over SQLAlchemy or an in-memory list so the module's injection-prevention/safe-query-building goal is actually exercised, with zero new dependencies.
- **2026-08-25** — Module 2 entity = `Item` (id, name, category, price, in_stock, created_at), kept independent from Module 1's `User` per the module-boundary rule.
- **2026-08-25** — `GET /items` with `page` beyond the last available page (or `pageSize` out of bounds) returns `400 FIELD_OUT_OF_RANGE`, not a silent clamp or bare 404.
- **2026-08-25** — Introduced a "composition root" pattern: `app/main.py` is the only file allowed to know about more than one module at once; cross-module reuse goes through a shared `core/ports` Protocol, with `main.py` injecting the concrete instance.
- **2026-08-25** — Module 3 (Import/Export & Background Jobs) uses a SQLite job table + async worker, `X-User-Id` header for user identity, and a 5 MB upload cap, reusing Module 1's User validation via the composition root.
- **2026-08-25** — Module 4 (Multi-Source Aggregation) uses Open-Meteo + the public GitHub API as sources, an in-memory TTL dict cache, and a partial-data-plus-warnings policy: essential sub-call failures are hard failures, enriching sub-call failures degrade to a 200 with a warning.
- **2026-08-25** — Adopted a versioned-folder repository layout: `V1/` holds the current runnable program as a frozen, rewindable snapshot; `CLAUDE.md`, `.claude/`, `ARCHITECTURE.md`, `CONTRACTS.md`, and `AGENT_LOG.md` stay at the project root as the shared, version-spanning source of truth. Future development happens in new version folders (`V2/`, etc.) alongside `V1/`, never by editing `V1/` in place.
- **2026-08-26** — V2 is architected as a fully static site (Option A): no backend, no database, deployable at $0 hosting cost (e.g. GitHub Pages), decided after auditing V1 for mutating endpoints and confirming Open-Meteo/GitHub both send open CORS headers.
- **2026-08-26** — V2's Imports module intentionally drops V1's async-job/polling/X-User-Id pattern in favor of synchronous client-side parse-validate-download, since a static site has no server to persist job state; this is a disclosed, approved scope change, not a silent regression.

## Logs
- [[REST API/logs/2026-08-25-module-1-2-complete|Module 1 2 complete]]
- [[REST API/logs/2026-08-25-module-3-4-complete|Module 3 4 complete]]
- [[REST API/logs/2026-08-25-v1-archival-and-cleanup|V1 archival and cleanup]]
- [[REST API/logs/2026-08-26-v2-static-port|V2 static port]]
