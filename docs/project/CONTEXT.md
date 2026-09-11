# Context

Use this file for durable project context that agents need across sessions.

## Project-Specific Facts

- Pure static HTML/CSS STEM learning-center website, grades 3–12; no JavaScript framework, no
  build tools, no package manifest, no CI, no external CDN/fonts/icon libraries anywhere in this
  repo. The one exception is a small vanilla-JS booking modal (open/close/fake-submit) present in
  `v0.2.5` and `v0.3.1` only — it selects elements only by `id`, never by class.
- Served by GitHub Pages from `docs/` on `main`. Live URL confirmed 2026-09-10:
  `https://rmz9dkfy5f-pixel.github.io/Summit-Learning-Center/` (`HTTP 200`).
- **`docs/index.html` is the actual live site root**, not merely a utility page — it is what the
  GitHub Pages URL above serves directly. It is a deliberate version picker (by explicit,
  repeated user decision, 2026-09-11) linking to each version folder — it does not, and should
  not, contain the STEM marketing content itself.
- Site content is versioned as `docs/vX.Y.Z/index.html` directories, navigated from
  `docs/index.html`. `v0.0.1`, `v0.1.4`, `v0.2.5`, `v0.3.1` exist on disk; several git tags
  (`v0.1.1`–`v0.1.3`, `v0.2.6`, `v0.2.7`) do not have a matching `docs/` folder — the tag history
  predates and is not fully explained by this session's work. Site version directories and git
  tags are tracked independently in this repo — a tag existing does not imply a matching
  directory, and vice versa.
- Site content dormant since 2026-04-08 until 2026-09-11, when `docs/v0.3.1/index.html` was added:
  a visual re-skin of `v0.2.5`'s exact same content onto a dark navy/blue-orange system — not a
  feature or content change. Migrated onto AntBrainOS Project Starter Kit v3.10.0 (profile
  `web_application`) on 2026-09-10 — a governance/tooling change, separate from both.

## Known Constraints

- Never edit or delete `docs/v0.0.1/` or `docs/v0.1.4/` — prior versioned directories are frozen.
- New site feature work starts a new `docs/vX.Y.Z/` directory copied from the latest version; no
  in-place edits to a shipped version.
- No JavaScript frameworks, npm, build pipeline, or external CDN dependencies for the site itself.

## Repeated Corrections

Add facts here when an agent makes the same mistake more than once.
