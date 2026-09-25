---
title: "Library templates — Decisions"
tags: [library-templates, decisions]
created: 2026-09-09
type: decisions
status: imported
---

# Decisions

- **2026-09-09** — Static HTML/CSS, no JS framework, no build step: the site is a simple card-grid vitrine, native HTML/CSS covers it.
- **2026-09-09** — The gallery site itself reuses precision-dark's own tokens rather than inventing a new aesthetic (confirmed via design-canvas's Phase A intake).
- **2026-09-09** — The agent performs no git actions whatsoever (init/add/commit/push/repo creation) and installs/downloads nothing outside this project's own `.venv` — explicit, standing user instruction. Git/GitHub/deploy steps are the user's to run themselves, and are not to be raised again as a pending item.
- **2026-09-09** — Each template's demo page shows the template's design tokens directly (style-guide/"kitchen sink" format: colour palette, font, font colour, style, block style and colour) rather than a fictional app mockup — grounded in research of real template-marketplace conventions, not invented from memory.
- **2026-09-09** — `assets/tokens.css` holds the gallery's own shared chrome; each template's page owns its own real token values. A `--page-*` variable set (site's light chrome: `--page-bg`, `--page-ink`, `--page-ink-muted`, `--page-border`) is kept distinct from a template's own `--color-*` variables (its real, accurate design tokens) — conflating the two caused two rejected background-fix attempts before this split was introduced.
- **2026-09-09** — Every page has one plain light background directly on `body`, with no wrapping "block"/frame div anywhere on any page, including the gallery. Only the specific demo elements that must show a dark template's real colours (swatches, type/style/block example panels) keep their own small, scoped dark backing.
- **2026-09-09** — Any translucent hover/active tint (`--hover-tint`, `--accent-tint`) must be layered over its element's own `--color-surface` via `background-color` + `background-image: linear-gradient(tint, tint)`, never a bare `background: var(--tint)` — the bare form replaces the surface color and breaks once the ambient page background changes.
- **2026-09-09** — Each template page also carries a "Composition guide" (features/components that fit naturally, plus short non-exhaustive avoid-lists for blocks and fonts), authored first in the template's own `.claude/skills/design-canvas/templates/<name>/composition.md` as source of truth, then rendered on the page — keeping the website a presentation layer over the skill's template library, never a divergent duplicate.
- **2026-09-09** — material-design-3 was built out as the second full template (not a new from-scratch idea), applying the precision-dark lessons (token-showcase format) from the start. Category: shopping/e-commerce list. Seed color: Google's own published M3 baseline purple (#6750A4), sourced from a real fetched reference table, not generated.
- **2026-09-10** — A throwaway static "maquette" (single HTML/CSS snippet, screenshotted to PNG) is now a mandatory direction-check step before building any full template mockup, going forward.
- **2026-09-10** — Any new template beyond precision-dark gets a fully self-contained stylesheet (own `:root`, own header/footer/tag rules, no link to `assets/tokens.css`), following material-design-3's precedent rather than precision-dark's shared-token approach.
- **2026-09-10** — Gallery template cards are themed per-template (modifier classes overriding only the shared custom properties the base card rule already reads) instead of all sharing precision-dark's dark chrome; precision-dark's own card is intentionally left unmodified since that dark chrome already is its theme.
- **2026-09-10** — Beyond performing no git actions, git/GitHub/deploy topics are not to be raised in conversation at all (not listed as pending items, reminders, or discussion points) — standing instruction, expands the 2026-09-09 no-git-actions decision.

## Logs
- [[Library templates/logs/2026-09-09-chip-fix-and-background-rework|Chip fix and background rework]]
- [[Library templates/logs/2026-09-10-warm-tactile-and-card-theming|Warm tactile and card theming]]
