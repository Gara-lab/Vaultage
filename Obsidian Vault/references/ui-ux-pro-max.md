---
title: "UI/UX Pro Max (Claude Code skill)"
tags: [design, ux, claude-code, skill, reference-library]
created: 2026-09-16
updated: 2026-09-16
status: active
type: reference
---

# UI/UX Pro Max

A Claude Code skill (design-intelligence database: UI styles, color palettes, font
pairings, UX guidelines, searched via a local Python script) —
https://github.com/nextlevelbuilder/ui-ux-pro-max-skill. Verified real and actively
maintained as of 2026-09-16. The upstream repo bundles 6 other skills alongside it
(banner-design, brand, design, design-system, slides, ui-styling) — only `ui-ux-pro-max`
itself has been used anywhere so far.

**Installed:** `Codex_V1/.claude/skills/ui-ux-pro-max/` (project-scoped, per explicit
user request — not the user-level `~/.claude/skills/`, so it does not apply to any other
project). Runs stdlib-only, no extra `.venv` packages needed; confirmed working
2026-09-16. If another project wants this too, it needs its own explicit install
decision (per-project copy, or promote to `~/.claude/skills/` for every project) —
this is not currently shared automatically.

The other candidate discussed alongside this one, "UX Patterns for Devs," could not be
matched to one specific canonical skill/repo as of 2026-09-16 — do not install anything
under that name without confirming the exact source first.

## Related links

- [[design-inspiration]]
