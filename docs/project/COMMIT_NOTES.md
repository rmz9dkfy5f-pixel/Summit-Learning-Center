# Commit Notes

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
