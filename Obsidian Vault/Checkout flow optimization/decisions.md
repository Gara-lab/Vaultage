---
title: "Checkout flow optimization — Decisions"
tags: [checkout-flow-optimization, decisions]
created: 2026-08-28
type: decisions
status: imported
---

# Decisions

- **2026-08-28** — Deliverable format is a single static HTML page (no build step, no backend), matching the Static_projects folder convention and keeping diagrams/narrative/calculator visually connected.
- **2026-08-28** — Illustrative data is sourced from Baymard Institute checkout-abandonment research, framed around a mid-size DTC apparel retailer persona (~100k monthly checkout starts) rather than fabricated real company data.
- **2026-08-28** — The what-if calculator stays a simple inline widget (no charts, no saved scenarios) to keep scope proportional to a portfolio piece.
- **2026-08-28** — Flow diagrams are authored in Mermaid.js (CDN-rendered, source kept in `.mmd` files) rather than static images, so they stay text-editable with no build step.
- **2026-08-28** — For static, no-build-step projects, default to a CSS framework that works via a single pinned CDN `<link>` with no JS runtime and no Node/npm pipeline. DaisyUI was rejected for this project because even its CDN path loads Tailwind's in-browser JIT runtime (`@tailwindcss/browser@4`); Pico.css was adopted instead (classless-capable, ~7.7kB gzipped, supports automatic light/dark mode). Water.css/Simple.css are acceptable leaner alternatives. Reserve DaisyUI for future projects that already accept a full npm/Tailwind build pipeline.
- **2026-08-28** — All user-visible headings, labels, and diagram step names use sentence case (not Title-Case-every-word), and no technical-looking ID codes (e.g. "PP-1") are shown to end users — cross-references between prose and diagrams/tables are done by matching step-name text alone.
- **2026-08-28** — The site's custom accent color (~#2f5d8a) is kept layered on top of Pico.css's default theme rather than adopting Pico's own default color, by overriding Pico's `--pico-primary` CSS variables through Pico's own selector patterns (required because Pico's theme selectors outrank a plain `:root` override on specificity).

## Logs
- [[Checkout flow optimization/logs/2026-08-28-pico-redesign-and-casing-cleanup|Pico redesign and casing cleanup]]
