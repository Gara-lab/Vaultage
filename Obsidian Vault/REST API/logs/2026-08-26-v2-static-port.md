---
title: "REST API — V2 static architecture audit and port"
tags: [rest-api, session-log]
created: 2026-08-26
type: session-log
status: imported
---

# V2 static architecture audit and port

## Summary
Audited whether V2 could be deployed as a fully static site (no backend, no DB, $0 hosting) by checking V1 for mutating endpoints, live CORS headers on Open-Meteo/GitHub, and per-module portability; recommended and got approval for Option A (fully static). Ported all four V1 modules (Transform, Items, Imports, Aggregate) from Python into vanilla JS `domain/` modules with no build step, including a hand-rolled CSV parser, AbortController-based fetch timeout, and a Map-based TTL cache mirroring V1's `MemoryCache`. Rewired all four page modules (via the Workflow tool, in parallel, with a single batched review) to call the new local domain logic instead of hitting a backend, and redesigned the Imports page from V1's async-job/polling pattern to a synchronous parse-validate-download flow since there is no server left to hold job state. Verified the whole port live with an offline Playwright smoke test (V2 served statically, zero calls to V1, real calls to Open-Meteo/GitHub including a cache-hit-on-repeat check and not-found cases) and closed out with `goal-evaluator: ok`. Cleaned up the now-dead `api.js` (old `fetchJson` helper) that the evaluator flagged as unused.

## Decisions
- Chose Option A: V2 is fully static (no backend, no DB), deployable to something like GitHub Pages at $0 hosting cost.
- Imports module intentionally dropped the async-job/polling/X-User-Id pattern in favor of synchronous client-side processing, since a static site has no server to persist job state — disclosed and approved as a scope change, not a silent regression.
- GitHub Pages deployment itself (git init/remote/Pages config) stays explicitly out of scope until separately requested.

## Open items
- Actually deploying V2 to GitHub Pages has not been started and needs its own explicit go-ahead before touching git/remote/Pages configuration.

## Files touched
- `V2/ui/data/items.json` (new — static snapshot of V1's seeded items catalog)
- `V2/ui/js/domain/errors.js`, `user.js`, `items.js`, `importProcessing.js`, `httpRetry.js`, `cache.js`, `openMeteo.js`, `github.js`, `aggregate.js` (new — ported V1 business logic)
- `V2/ui/js/pages/transform.js`, `items.js`, `imports.js`, `aggregate.js` (rewired to use `domain/`, base-URL/X-User-Id inputs removed)
- `V2/ui/js/api.js` (deleted — dead code after rewiring)
- `ARCHITECTURE.md`, `CONTRACTS.md`, `AGENT_LOG.md` (updated to document the static architecture and imports scope change)
