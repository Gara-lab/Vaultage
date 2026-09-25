---
title: "Employee recognition wall — Decisions"
tags: [employee-recognition-wall, decisions]
created: 2026-09-14
type: decisions
---

- **2026-09-14** — Chose a single `index.html` (inline CSS/JS) as the initial architecture, later superseded by adding a minimal Flask server (`server.py`) + `data/recognitions.json` once admin-added nominations needed to persist for all visitors — a pure static file has nowhere to write shared state.
- **2026-09-14** — Admin "add a name" feature is gated by a shared passphrase, checked client-side and server-side (`X-Admin-Passphrase` header). This is explicitly a deterrent, not real authentication, per the user's own choice of "simple gate" over real auth — no hashing, sessions, or rate limiting.
- **2026-09-14** — French translation covers UI chrome only, not nomination text, per the user's explicit choice; each nomination stays in whichever language it was submitted in.
- **2026-09-14** — Avatars are deterministic hash-derived SVGs. Added a required "Gender" field (admin form only, never shown publicly) so avatars read as the correct gender for people who don't want their real photo shown, instead of a random hairstyle. Real entries missing the field (e.g. "Burman") fall back gracefully rather than being guessed.
- **2026-09-14** — Category and Service are two independent, combinable (AND) filter groups rather than one flat list, matching the user's request that categories live "within the Category tag" as a labeled group, with Service (MB, SOCLE, Error PDL/Erreur PDL, FAC, SUB/SOUS, CONF, QUAL) as a second group. Unlike Gender, the Service value IS shown on public cards as a secondary tag — a judgment call flagged to the user, not an explicit request.
- **2026-09-14** — Standing rule established twice (gender, then service): never guess or backfill a personal attribute for a real user-submitted entry ("Burman"); only backfill for fictional sample entries invented during development. Real entries missing a field must degrade gracefully (no tag, no avatar guess), never crash or assume a value.
