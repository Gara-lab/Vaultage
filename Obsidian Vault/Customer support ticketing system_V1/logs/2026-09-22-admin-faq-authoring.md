---
title: "Customer support ticketing system_V1 — Admin-only FAQ authoring"
tags: [customer-support-ticketing-system-v1, session-log]
created: 2026-09-22
type: session-log
status: imported
---

# Admin-only FAQ authoring

## Summary
Built a full Admin-only FAQ management layer on top of the existing public knowledge base. The public FAQ page (`kb.html`) now filters articles through a 4-option pill (Getting started / Your ticket / IT questions / HR questions) reusing the site's existing pill CSS, driven by a new `categoryKey` slug on each article instead of an inline bilingual category string. A new `admin/faq.html` + `js/faq-admin.js` page (gated the same way as `admin/team.html`) lets Admin add or remove FAQ entries in any of the 4 categories; this page deliberately has no `hr/`/`it/` counterpart since FAQ authorship is Admin-only. Admin-submitted content is stored via a new `js/kb-store.js` module (sole owner of the `helpdesk:kbArticles` localStorage key, with its own Node self-check) and merged with the static seed articles from `data/kb.js` at render time. Went through the full propose → 3 clarifying questions → user approval ("Go") → implementation → Playwright verification → `goal-evaluator` Completion Loop, which returned `VERDICT: ok`.

## Decisions
- Single-language admin input: admin-submitted question/answer are plain strings (not `{fr,en}` pairs like the static seed content) and are shown identically regardless of site language, per the user's chosen "single language, mirrored" option.
- Admins can delete FAQ entries they've added (not just add), per the user's chosen "allow delete" option.
- An admin can file a new FAQ entry into any of the 4 categories, not just the 2 new ones, per the user's chosen option.
- `admin/faq.html` is intentionally not copied into `hr/`/`it/` — FAQ management is an Admin-only surface, breaking from the otherwise-identical 4-page admin/hr/it template convention.

## Open items
None — task fully implemented, documented across ARCHITECTURE.md/CONTRACTS.md/CODE_MAP.md/AGENT_LOG.md, and evaluator-approved.

## Files touched
- `data/kb.js` — categoryKey refactor
- `js/kb-store.js` (new) + `js/kb-store.test.js` (new)
- `js/kb.js` — pill filter + merge logic
- `kb.html` — pill markup + new script tag
- `js/i18n.js` — new nav/category/admin-form keys
- `admin/faq.html` (new) + `js/faq-admin.js` (new)
- `admin/dashboard.html`, `admin/team.html`, `admin/ticket.html` — new FAQ nav link
- `ARCHITECTURE.md`, `CONTRACTS.md`, `CODE_MAP.md`, `AGENT_LOG.md` — spec/log updates
