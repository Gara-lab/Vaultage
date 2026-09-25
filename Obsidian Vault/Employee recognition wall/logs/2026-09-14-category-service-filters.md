---
title: "Employee recognition wall — Category/Service filters, admin gate fix, gendered avatars"
tags: [employee-recognition-wall, session-log]
created: 2026-09-14
type: session-log
status: imported
---

# Category/Service filters, admin gate fix, gendered avatars

## Summary
Built the Employee Recognition Wall as a single-page appreciation dashboard via `design-canvas` + ponytail, then evolved it from a static `index.html` into a frontend + minimal Flask backend (`server.py`, `data/recognitions.json`) so admin-added nominations persist for everyone. Added a passphrase-gated admin "add a name" feature and an English/French UI toggle, then fixed a bug where the passphrase error only showed on form submit instead of immediately on "Unlock" (via a new `/api/verify-passphrase` endpoint). Added a required Gender field to the admin form (admin-only, never shown publicly) so generated 2D vector avatars match the chosen gender instead of being random. Most recently, restructured the single filter nav into two independently-combinable, labeled filter groups — Category and a new Service/"Cellule-Service" dimension (MB, SOCLE, Error PDL/Erreur PDL, FAC, SUB/SOUS, CONF, QUAL) — added as a required admin-form field and a visible secondary tag on cards. `goal-evaluator` signed off on all tasks (verdict: ok).

## Decisions
- See `decisions.md` for the durable ones (architecture change, simple-gate-not-real-auth, French UI-only translation, gender/service no-guess rule, Service tag visibility judgment call).

## Open items
- User started a request ("in the current example, there is the name of the city right after the...") but it was interrupted by an accidental click; explicitly told not to act on it until restated.
- Whether the Service tag should stay visible on public cards (vs. hidden like Gender) was flagged to the user as a judgment call, not yet explicitly confirmed either way.

## Files touched
- `index.html`
- `server.py`
- `data/recognitions.json`
- `requirements.txt`
- `ARCHITECTURE.md`
- `CODE_MAP.md`
- `AGENT_LOG.md`
