---
title: "Customer support ticketing system_V1 — FR/EN language toggle"
tags: [customer-support-ticketing-system-v1, session-log]
created: 2026-09-22
type: session-log
status: imported
---

# FR/EN language toggle

## Summary
Reoriented the `Codex_V1` factory-root workspace onto `Customer support ticketing system_V1/` as its active project (removing an unrelated RWKV-7/stigmergy decision entry from the root `AGENT_LOG.md` and staging unnecessary duplicated tooling into a `Remove/` subfolder, per the established convention). Used `/design-canvas` and ponytail (full) to design and build a French/English language toggle covering all 7 pages of the site, with French as the default and the choice persisted in `localStorage`. Built a hand-written `js/i18n.js` STRINGS dictionary (no library) driving `data-i18n`/`data-i18n-placeholder` HTML attributes plus direct `I18N.t()` calls for dynamic JS-rendered content, including the 5 KB articles and the admin setup-mode passphrase copy. The toggle's pill UI reuses the site's existing `.pill-option` CSS pattern. Verified end-to-end with live Playwright browser tests (default-French, toggle-to-EN with reload, cross-page persistence, KB translation, admin login flow, dashboard header/row translation). Ran the Completion Loop twice via `goal-evaluator`: the first pass caught a false "reuse" claim (a duplicate CSS class set had been built instead of a genuine `.pill-option` modifier) which was fixed; the second pass returned `VERDICT: ok`.

## Decisions
- See `decisions.md` for the durable ones (project lineage note, i18n architecture, KB bilingual-pair exception, `.pill-option` reuse rule).

## Open items
- User still has a `Remove/` folder inside `Customer support ticketing system_V1/` to manually delete whenever ready (staged, not deleted, per convention).

## Files touched
- `Codex_V1/AGENT_LOG.md` (removed stale decision, added focus-change entries)
- `Customer support ticketing system_V1/Remove/` (new — staged duplicate tooling)
- `Customer support ticketing system_V1/js/i18n.js` (new)
- `Customer support ticketing system_V1/js/format.js`, `js/kb.js`, `js/dashboard.js`, `js/status-lookup.js`, `js/ticket-form.js`, `js/ticket-detail.js`, `js/team.js`, `js/admin-login.js`
- `Customer support ticketing system_V1/data/kb.js`
- All 7 HTML pages (`index.html`, `status.html`, `kb.html`, `admin/login.html`, `admin/dashboard.html`, `admin/team.html`, `admin/ticket.html`)
- `Customer support ticketing system_V1/css/styles.css`
- `Customer support ticketing system_V1/ARCHITECTURE.md`, `CONTRACTS.md`, `CODE_MAP.md`, `AGENT_LOG.md`
