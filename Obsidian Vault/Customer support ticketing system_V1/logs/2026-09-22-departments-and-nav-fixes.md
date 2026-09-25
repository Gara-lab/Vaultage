---
title: "Customer support ticketing system_V1 — admin-session fix, HR/IT departments, nav fixes"
tags: [customer-support-ticketing-system-v1, session-log]
created: 2026-09-22
type: session-log
status: imported
---

# Admin-session fix, HR/IT departments, nav fixes

## Summary
Fixed a bug where returning to Admin after visiting the public site re-prompted for the passphrase even without logging out; the first attempt (a body-script guard) still let the login form flash on screen for a moment, so the real fix moved the login-state check into a blocking `<head>` script in `admin/login.html`. Renamed "Knowledge base" to "FAQ" site-wide (FR/EN). Added two new departments, HR and IT, that work exactly like Admin but fully independently (own ticket queue, own team roster, own login/passphrase session), reachable via a new "Espace équipe" dropdown in the nav replacing the old single Admin link; this required refactoring `js/store.js` and `js/admin-auth.js` to take an explicit `department` argument and adding `js/department.js` to resolve the current department from the URL path. Finally added a "Submit" nav link back to the ticket form (since clicking the brand link wasn't intuitive) and renamed "Check ticket status" to just "Status" everywhere, catching and fixing a stale reference to the old label inside a `data/kb.js` FAQ answer along the way. Every task went through the project's Completion Loop (`goal-evaluator`), including one real block/fix cycle when `js/store.test.js` was found still using pre-department call signatures.

## Decisions
- Passphrase/login-state checks that must prevent any flash of protected content belong in a blocking `<head>` script (`window.location.replace(...)` before `<body>` parses), not a body-bottom script — the latter is not sufficient even though it is logically correct, since the DOM still paints before it runs.
- HR and IT departments are structurally identical to Admin but fully isolated: separate ticket queues, separate team rosters, separate login/passphrase sessions per department. Chosen over shared-queue/shared-roster/nav-toggle alternatives per explicit user selection (Recommended options: separate queues, separate rosters, dropdown menu).
- Department scoping is resolved from the URL path (`.../admin/login.html` → `"admin"`) via `js/department.js`, and passed explicitly into `Store`/`AdminAuth` functions rather than having those modules self-resolve it — keeps them usable from both department-scoped pages and public pages (ticket form, status lookup).
- With no build step available, `hr/` and `it/` are maintained as content-identical byte-copies of `admin/`'s HTML files (one `data-i18n` key + label text differs per file), verified after each edit via `diff` rather than any automated drift check.
- Department-specific display strings (nav brand, login title) use separate literal i18n keys per department (`nav.hrBrand`, `hr.loginTitle`, etc.) rather than runtime interpolation, since `data-i18n`'s attribute-driven `apply()` doesn't support passing variables into a lookup.

## Open items
None outstanding — the most recent request (Submit nav link + Status rename) passed its `goal-evaluator` check (VERDICT: ok). The `Remove/` folder inside the project root remains staged for the user to delete manually whenever ready (unrelated background item, not acted on this session).

## Files touched
- `js/admin-login.js`, `js/admin-auth.js`, `js/store.js`, `js/department.js` (new)
- `js/dashboard.js`, `js/team.js`, `js/ticket-detail.js`, `js/ticket-form.js`, `js/status-lookup.js`
- `js/i18n.js`
- `admin/login.html`, `admin/dashboard.html`, `admin/team.html`, `admin/ticket.html`
- `hr/login.html`, `hr/dashboard.html`, `hr/team.html`, `hr/ticket.html` (new)
- `it/login.html`, `it/dashboard.html`, `it/team.html`, `it/ticket.html` (new)
- `index.html`, `status.html`, `kb.html`
- `css/styles.css`
- `data/kb.js`
- `ARCHITECTURE.md`, `CONTRACTS.md`, `CODE_MAP.md`, `AGENT_LOG.md`
- `js/store.test.js`
