---
title: "Customer support ticketing system — decisions"
tags: [customer-support-ticketing-system, decisions]
created: 2026-09-11
type: decision-log
---

# Decisions

- **2026-09-11** — Pure static site: HTML/CSS/vanilla JS only, no framework, no build step, no backend/API. Required because the site must be hosted on static hosting with no server and no external dependencies.
- **2026-09-11** — Ticket and agent data live in browser `localStorage` only, scoped to a single browser/device (not shared across users or devices) — direct consequence of the static-only constraint; user explicitly chose this over any shared-storage alternative.
- **2026-09-11** — No automatic email notifications for ticket status changes — user explicitly chose to drop this rather than use `mailto:` or an external email API, since static hosting has no backend to send mail from.
- **2026-09-11** — Admin login is a client-side passphrase gate, not real access control, and is documented as such directly in the UI — static hosting cannot enforce server-side auth.
- **2026-09-11** — Knowledge base content is static data in `data/kb.js` (a plain JS global), not a fetched JSON file and not an admin-editable CRUD feature — avoids `fetch()` CORS issues when opened via `file://`, and requirements only asked for a public KB, not authoring tooling.
- **2026-09-11** — Team member management is a separate `admin/team.html` page rather than part of the dashboard — user's explicit choice when asked how to split up the admin UI.
- **2026-09-11** — Ticket priority is shown as color-coded pills/tags throughout the admin UI — user's explicit choice during design-canvas's direction-check step.
- **2026-09-13** — Split the mixed project root into two independent sibling clones, `coding-clone/`
  (the static ticketing site's own harness) and `video-clone/` (the unrelated video-production
  pipeline's own harness), each with its own full `.claude/`, CLAUDE.md, ARCHITECTURE.md,
  CONTRACTS.md, AGENT_LOG.md, CODE_MAP.md, HOW_TO_USE.md, skills, and a freshly bootstrapped empty
  `.venv` — rather than keeping the awkward "Scope guard" arrangement where one CLAUDE.md told the
  agent to ignore a dormant, accidentally-merged video pipeline sitting in the same root. The
  original root was left untouched; the user intends to relocate each clone to its own project
  location later.
- **2026-09-14** — `Short1HelpdeskDesktop.tsx` keeps the same `DeviceMockup` outro as
  `Short1Helpdesk.tsx` after all, reversing the earlier "no outro" scoping decision — final call
  after debate.
- **2026-09-14** — The two split-out clones (now relocated to
  `...\Bureau\AI\system_workflow_template\Codex_V1` and `...\Luminara_V1`) are treated as living
  master templates: durable process/craft lessons learned in this project get fed back into their
  `CLAUDE.md`/skill files (scoped to each clone's own domain), not just recorded here.
