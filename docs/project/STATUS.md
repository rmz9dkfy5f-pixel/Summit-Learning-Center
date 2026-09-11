# Status

## Current State

Static HTML/CSS STEM learning center site (grades 3–12), served from `docs/` via GitHub Pages.
Site content was dormant since 2026-04-08 (previous latest published version:
`docs/v0.2.5/index.html`) until this push, which adds a new published version and redesigns the
site root. Final pushed commit `d82ecc087a83a8a77f0c0674805dca7b537fd20d`, tagged `v0.3.1` (tag
pushed: yes; remote tag verified: yes). Snapshot created and verified at
`/Users/ant/WorkSync/Projects/RepoBackups/Summit-Learning-Center/v0.3.1/`.

## Last Updated

2026-09-11 (later session) — **`docs/index.html` visual re-architecture.** Full-bleed centered
hero replacing the two-column hero and its absolutely-positioned decorative stage; the latest
release promoted to a full-width row above a 3-up row of archived releases; the 3-stat strip
relocated to a closing band. All decorative emoji replaced with inline SVG (`<symbol>` sprite,
`currentColor`). Expressive CSS-only motion added — staggered entrances, a continuously rotating
conic ring, drifting hero orbs, and a breathing recency dot on the latest release — behind a
`prefers-reduced-motion` guard. **Zero content change: all 49 user-visible strings are byte-identical
to the previous version.** No JavaScript, no external references. Two pre-existing defects fixed in
the same pass: `.version-card:focus-visible { outline: none }` (keyboard users had no focus
indicator) and the fragile hero-stage geometry described under Broken/Unknown below, which is now
flow-based and collision-proof. Unverified browser rendering is **no longer** an open risk for this
file — see Working.

2026-09-11 — Landing-page visual redesign. Added `docs/v0.3.1/index.html`: a visual re-skin of
`v0.2.5`'s exact same content (hero, grade paths, programs, assessment, services, booking modal)
onto a dark navy/blue-orange visual system ported from a separate reference site's design
language — no content added, altered, or removed; only CSS and a new sticky nav (labels drawn
from existing section headings) changed. Redesigned `docs/index.html` (confirmed to be the live
site root) as a full-width, multi-section "infographic style" version picker — hero with a
decorative CSS-only stage (donut version-count ring, open-book centerpiece), a 2×2 versions grid,
and a 4-node release timeline — while keeping its exact existing content (title, lead, all 4
version labels/descriptions, footer note) unchanged. Updated
`docs/governance/REPOSITORY_HANDOFF_CONFIG.md` and this file with the confirmed GitHub Pages live
URL (`https://rmz9dkfy5f-pixel.github.io/Summit-Learning-Center/`, `HTTP 200`).

## Working

- **Verification performed for the `docs/index.html` re-architecture (later 2026-09-11 session),
  including the real-browser check that was previously outstanding.** Headless Microsoft Edge
  (`--headless=new`) screenshots inspected at 1600 / 1100 / 900 / 760 / 520 / 400 / 360 px: no
  horizontal overflow, no clipping, no element collisions at any width; the wide latest row
  collapses correctly at its 760px breakpoint and the 3-up grid reflows 3→2+1→1 via
  `auto-fit`/`minmax` without squeezed or orphaned columns; card CTAs stay aligned despite unequal
  body heights. String parity checked mechanically — 49 user-visible strings, multiset-identical
  before and after. HTML tag-balance clean. Local `python3 -m http.server` + `curl`: root and all 4
  version links return `HTTP 200`. Zero `<script>` tags and zero external references (no CDN, fonts,
  or `url()`) in the file. Rendering also confirmed with `prefers-reduced-motion` forced — nothing
  is left hidden.
  - Two bugs were found *by* this verification and fixed: the `prefers-reduced-motion` guard
    originally reset `animation-duration` but not `animation-delay`, so a reduced-motion visitor
    would have waited out the full entrance stagger looking at invisible content; and the latest
    release's 16/9 scene forced its row ~100px taller than its own text column, leaving the card
    looking half-empty.
  - Caveat on method: below roughly 400px, Windows clamps the headless browser's window width, so
    narrow viewports were verified through a 360px/400px `<iframe>` harness rather than by resizing
    the window. Screenshots were captured with reduced motion forced, because virtual-time and CSS
    animations race and made un-forced captures nondeterministic.
- Site content: `docs/v0.0.1/`, `docs/v0.1.4/`, `docs/v0.2.5/` unchanged and unaffected. New:
  `docs/v0.3.1/index.html`. `docs/index.html` redesigned (content unchanged, visual system
  rebuilt).
- GitHub Pages live URL confirmed: `https://rmz9dkfy5f-pixel.github.io/Summit-Learning-Center/`
  (`HTTP 200`).
- Verification performed this push (no test suite/build step exists in this repo — manual/scripted
  checks only): HTML tag-balance checks (regex open/close counts) on both new/changed files —
  clean; content-parity diffs against each file's pre-change committed version — zero dropped or
  altered lines, every newly-introduced string enumerated and reviewed; local `python3 -m
  http.server` + `curl` checks — root and all 4 version links return `HTTP 200`, zero external
  resource references (no CDN/fonts/scripts) in either changed file; booking modal `<script>`
  block confirmed byte-identical between `v0.2.5` and `v0.3.1`.

## Broken / Unknown

- `validate --release` is BLOCKED on facts that need a human decision, not something to infer:
  `public_exposure`, `data_sensitivity`, `risk_level` (`.starter-kit/project-profile.json`), and an
  explicit privacy/data classification disposition (`.starter-kit/privacy-classification.json`).
- ~~Actual browser rendering of the new `docs/index.html` decorative elements has not been visually
  confirmed.~~ **Closed (later 2026-09-11 session)** — verified in a real browser across seven
  widths; see Working above. The specific elements that were unverified (the CSS-only book shape,
  the floating pills) no longer exist: they were the fragile absolutely-positioned geometry and were
  replaced with flow-based layout. The conic ring survives, re-sited into normal flow, and renders
  correctly at every width checked.
- Not verified: rendering in Firefox or Safari. All checks were run in Chromium (Edge). The page
  uses only broadly-supported CSS — `color-mix()`, `aspect-ratio`, `conic-gradient`, and a
  `@supports`-guarded `background-clip: text` — but this has not been observed first-hand.

## Next Actions

- Decide and record the release-readiness facts above, or explicitly accept deferring them.
