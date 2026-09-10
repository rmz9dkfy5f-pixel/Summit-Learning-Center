# Context

Use this file for durable project context that agents need across sessions.

## Project-Specific Facts

- Pure static HTML/CSS STEM learning-center website, grades 3–12; no JavaScript, no build tools,
  no package manifest, no CI.
- Served by GitHub Pages from `docs/` on `main`. Live URL has never been confirmed (open item,
  predates this migration).
- Site content is versioned as `docs/vX.Y.Z/index.html` directories, navigated from
  `docs/index.html`. Only `v0.0.1`, `v0.1.4`, `v0.2.5` exist on disk; several git tags
  (`v0.1.1`–`v0.1.3`, `v0.2.6`, `v0.2.7`) do not have a matching `docs/` folder — the tag history
  predates and is not fully explained by this session's work.
- Site content dormant since 2026-04-08. Migrated onto AntBrainOS Project Starter Kit v3.10.0
  (profile `web_application`) on 2026-09-10 — a governance/tooling change, not a content release.

## Known Constraints

- Never edit or delete `docs/v0.0.1/` or `docs/v0.1.4/` — prior versioned directories are frozen.
- New site feature work starts a new `docs/vX.Y.Z/` directory copied from the latest version; no
  in-place edits to a shipped version.
- No JavaScript frameworks, npm, build pipeline, or external CDN dependencies for the site itself.

## Repeated Corrections

Add facts here when an agent makes the same mistake more than once.
