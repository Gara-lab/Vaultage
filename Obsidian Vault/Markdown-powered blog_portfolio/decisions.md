---
title: "Markdown-powered blog_portfolio — Decisions"
tags: [markdown-powered blog_portfolio, decisions]
created: 2026-09-04
type: decisions
---

# Decisions

- **2026-09-04** — Content split into `content/posts/*.md` (dated, listed, in RSS) and `content/pages/*.md` (undated, not in RSS): portfolio pages (About, Projects) shouldn't appear in the post feed.
- **2026-09-04** — Front matter is hand-parsed flat `key: value` lines instead of adding PyYAML: only title/date/tags/slug are ever needed, not full YAML.
- **2026-09-04** — RSS is built with stdlib `xml.etree.ElementTree` instead of a feed library: the format is simple enough that a dependency isn't justified.
- **2026-09-04** — `output/` is never deleted/wiped before a build, only created if missing and overwritten in place: this project's filesystem (OneDrive-synced corporate folder) denies all delete operations at the OS ACL level (`icacls` confirms an inherited DENY ACE for Delete-Child/Synchronize on the whole tree), so `shutil.rmtree` reliably raises `PermissionError` here. This is an environment constraint, not a design preference — it will recur in any other project stored under this same OneDrive tree.
- **2026-09-04** — Dev server (`python main.py serve`) uses stdlib `http.server` + mtime polling instead of a filesystem-event library (`watchdog`): a personal dev server doesn't need push-based notification.
- **2026-09-04** — `serve()`'s rebuild step never lets a build error crash the server: editors create-then-write, so the poll can catch a `.md` file mid-write and hit a transient parse error. `_rebuild()` catches and logs instead of propagating, since the next poll naturally retries.

## Logs
- [[Markdown-powered blog_portfolio/logs/2026-09-04-build-and-crash-fix|Build and crash fix]]
