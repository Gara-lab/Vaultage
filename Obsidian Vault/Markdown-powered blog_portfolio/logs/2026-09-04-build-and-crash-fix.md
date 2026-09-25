---
title: "Markdown-powered blog_portfolio — build, ponytail cleanup, dev server, crash fix"
tags: [markdown-powered blog_portfolio, session-log]
created: 2026-09-04
type: session-log
status: imported
---

# Build, ponytail cleanup, dev server, crash fix

## Summary
Built the full static site generator end to end this session: `ssg/content.py` (front-matter parsing, `Post`/`Page` discovery), `ssg/render.py` (Markdown→HTML with TOC/codehilite via extensions, Jinja2 rendering), `ssg/feed.py` (stdlib RSS), and `ssg/build.py`/`main.py` (orchestration + CLI). Hit and root-caused a real environment constraint: this OneDrive-synced project folder denies all filesystem delete operations, which forced `run()` to be redesigned delete-free. Ran a ponytail over-engineering audit on request, applied the two findings that didn't require deleting a file (inlined single-caller render wrappers; had `Post` inherit `Page` via `field(kw_only=True)` instead of duplicating fields). Added a leaner `serve()` dev server (stdlib `http.server` + mtime polling, no new file) after a ponytail pass on that plan too. During a live demo, a newly created content file crashed the server (editor create-then-write race caught mid-write by the poll); root-caused and fixed with a `_rebuild()` exception-wrapping helper, verified by direct reproduction and by an independent `enforcer` subagent pass, with new automated test coverage added.

## Decisions
See `decisions.md` in this project folder — six decisions captured there, most durable one being the OneDrive delete-restriction, which will resurface in other projects under this same OneDrive tree.

## Open items
- Four leftover demo/test content files remain in `content/posts/` (`whatever.md`, `crash-test.md`, `oneshot-bad.md`, `repro-empty.md`) — all have valid front matter now so they won't break the build, but they aren't real posts. This environment can't delete them; user needs to remove them manually via File Explorer.
- Unclear (not tested either way) whether the OneDrive delete-restriction would also block the user's own manual deletion via File Explorer — worth the user checking.
- Two ponytail-audit findings were left unapplied because they require deleting a file: merging `templates/post.html` + `templates/page.html`, and removing the unwired `check_duplication.py` hook.
- Previously-listed "not yet supported" features (drafts, pagination, image handling, theming, a site config file) remain unimplemented and unrequested — no action needed unless the user asks.

## Files touched
- `ssg/content.py`, `ssg/render.py`, `ssg/feed.py`, `ssg/build.py`, `main.py`
- `test_build.py`
- `templates/base.html`, `templates/post.html`, `templates/page.html`, `templates/index.html`, `static/style.css`
- `content/posts/hello-world.md`, `content/pages/about.md` (plus leftover demo files listed above)
- `ARCHITECTURE.md`, `CODE_MAP.md`, `AGENT_LOG.md`
- `README.md`, `HOW_TO_USE.md`, `.script/setup-venv.ps1` (path-reference fixes)
