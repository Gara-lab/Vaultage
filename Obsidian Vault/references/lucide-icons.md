---
title: "Lucide icon library"
tags: [icons, design-system, reference-library]
created: 2026-09-16
updated: 2026-09-16
status: active
type: reference
---

# Lucide icon library

A local, offline copy of the [Lucide](https://lucide.dev) icon set (`lucide-static`
v1.46.0, ISC license), kept here so any project can pull a single icon without adding
a dependency or a build step.

## What's here

- `lucide-icons/sprite.svg` — all 2,102 icons as `<symbol id="...">` defs in one 500KB
  file (`<symbol id="a-arrow-down">`, etc. — kebab-case Lucide icon names).
- `lucide-icons/tags.json` — icon name → search keywords, for finding the right icon by
  concept (e.g. `"ticket"`, `"trash"`, `"filter"`) without browsing lucide.dev.
- `lucide-icons/LICENSE` — ISC, ship with any project that uses an icon from this set.

## How a project should use this

This is a **design-time source, not a runtime dependency**. Never point a shipped
project at this path, and never add `lucide` / `lucide-react` / `lucide-static` as an
npm dependency just to get one icon.

1. Open `lucide-icons/sprite.svg`, find the `<symbol id="...">` for the icon needed
   (use `tags.json` to find the name if the exact icon isn't obvious).
2. Copy that `<symbol>`'s inner `<path>` elements into a small standalone `<svg
   viewBox="0 0 24 24">...</svg>` directly in the consuming project's own HTML/CSS/JS —
   self-contained, no external reference, no build step, no network call at runtime.
3. Keep the ISC license notice wherever the project already tracks third-party asset
   credits (e.g. its `CODE_MAP.md` or a `THIRD_PARTY_LICENSES` note).

## Related links

- [[lucide-icons]] (this note)
- Upstream: https://lucide.dev · https://github.com/lucide-icons/lucide
