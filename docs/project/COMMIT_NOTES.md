# Commit Notes

## 2026-09-12 — Firefox/WebKit cross-browser visual check (documentation only, no site-code change)

## Summary

- Verified `docs/index.html` (unchanged since `v0.3.2`) renders correctly in real headless Firefox
  155.0 and in Playwright's WebKit engine (an explicitly-labeled Safari proxy, not genuine Apple
  Safari), at the same 7 widths as the earlier Edge check. Zero overflow, layout matches the
  already-verified Chromium/Edge pass. Updated `docs/governance/COMPATIBILITY_MATRIX.md` and this
  file's sibling `docs/project/STATUS.md` with the results.

## Description

- What changed: no change to `docs/index.html` or any site content — this was a verification-only
  pass. Only `docs/governance/COMPATIBILITY_MATRIX.md` and `docs/project/STATUS.md` were updated
  with the confirmed browser-coverage results.
- Why: user-confirmed next task from the prior session's closeout — the Firefox/Safari visual
  check that had been left open.
- Validation: Playwright-driven headless Firefox and WebKit, 7 widths
  (1600/1100/900/760/520/400/360px), both `prefers-reduced-motion: reduce` and default —
  `document.documentElement.scrollWidth` measured against viewport width at every combination (28
  captures total), zero overflow. Screenshots at representative widths (1600, 760, 360) reviewed
  for both engines — layout, reflow, and CSS-feature rendering (`conic-gradient`, `color-mix()`,
  `aspect-ratio`, `@supports`-guarded `background-clip: text`) all matched the already-verified
  Chromium/Edge pass.
- Risks / follow-up: the Safari result is a WebKit-engine proxy, not genuine Apple Safari — real
  Safari verification remains open and needs actual Mac hardware.

## 2026-09-11 (third session) — `docs/index.html` re-architecture + background icon field (will be tagged `v0.3.2`, applied in this session's closeout)

## Summary

- Re-architect `docs/index.html`'s IA (full-bleed hero, promoted latest release, inline SVG icons,
  CSS-only motion) — commit `c5e999d` — then add a whole-page educational icon background field —
  commit `3976428`.

## Description

- What changed: `c5e999d` replaced the two-column hero and its fragile absolutely-positioned
  decorative stage with a full-bleed centered layout, promoted the latest release to a full-width
  row above a 3-up archived-release grid, replaced all emoji with inline SVG (`<symbol>` sprite),
  and added staggered/rotating/breathing CSS motion behind a `prefers-reduced-motion` guard — fixing
  a pre-existing `outline:none` accessibility regression along the way. `3976428` added a decorative
  whole-page background field of 9 education-themed inline SVG icons (~19 instances: cap, flask,
  sigma, book, pencil, apple, diploma/scroll, atom, ruler) across every section, stroke-only at
  0.10–0.18 opacity, painting behind all foreground content. Both commits: zero user-visible copy
  change (49 strings verified byte-identical throughout), no JavaScript, no external references.
- Why: user requested the visuals be "enhanced considerably" after seeing the shipped v0.3.1
  picker, then separately asked for the background to feel less "plain and bland" with educational
  imagery — both refined through direct back-and-forth on IA ambition, icon style, motion, and
  copy-change scope.
- Validation: real-browser (headless Edge) passes at 1600/1100/900/760/520/400/360px for both
  commits — the 400/360px widths via a same-origin `<iframe>` harness with direct
  `document.documentElement.scrollWidth` measurement, since Windows clamps headless browser windows
  narrower than ~400px. String-parity check (49/49 unchanged), HTML tag-balance, zero
  `<script>`/external-reference check, and `python3 -m http.server` + `curl` HTTP 200 checks on all
  4 version links, for both commits. Both were also verified live in production after deploy
  (byte-for-byte match between the committed blob and the deployed page).
- Risks / follow-up: only Chromium has been observed — no Firefox/Safari visual check yet (recorded
  as this closeout's confirmed next task). `validate --release` remains BLOCKED on pre-existing,
  unrelated release-readiness facts (`public_exposure`, `data_sensitivity`, `risk_level`, privacy
  classification).

## 2026-09-11 — Landing-page visual redesign (will be tagged `v0.3.1`)

## Summary

- Add `docs/v0.3.1/index.html` (visual re-skin of `v0.2.5`) and redesign `docs/index.html` (the
  live site root) into a full-width, multi-section version-picker page.

## Description

- What changed: `docs/v0.3.1/index.html` ports a dark navy/blue-orange visual system, a sticky
  nav, and a relocated KPI-style stat row onto `v0.2.5`'s exact existing content — no copy added,
  altered, or removed, and its booking-modal JS is byte-identical to `v0.2.5`'s. `docs/index.html`
  — confirmed this session to be what the deployed GitHub Pages URL actually serves — was rebuilt
  from a single boxed card into hero / versions-grid / release-timeline sections, using only
  verified facts and existing text (no per-version ratings or invented feature claims).
  `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` and `docs/project/STATUS.md` record the now
  confirmed GitHub Pages live URL.
- Why: user-requested landing-page visual redesign, refined over several rounds into redesigning
  the actual site root rather than a secondary version page.
- Validation: HTML tag-balance checks, content-parity diffs against each file's pre-change
  committed version (zero dropped/altered lines), local `http.server` + `curl` checks (root and
  all 4 version links `HTTP 200`, zero external resource references), booking-modal script
  byte-diff (identical). No real-browser visual check was possible in the build environment.
- Risks / follow-up: new decorative CSS in `docs/index.html` (conic-gradient ring, CSS-only book
  shape, new breakpoints) is unverified visually — recommend a human browser check, especially at
  the ~880/720/640/520px breakpoints. `validate --release` remains BLOCKED on pre-existing,
  unrelated release-readiness facts.

## Suggested Commit Template

```text
<type>: <short summary>

- What changed:
- Why:
- Validation:
- Risks:
```

## Commit Types

- feat
- fix
- docs
- refactor
- test
- chore
- security
- perf
