# Compatibility Matrix

Use this for web, desktop, mobile, CLI, game, server, and automation projects.

## Platforms

| Platform | Required? | Status | Notes |
|---|---:|---|---|
| Windows | TBD | Unknown | |
| macOS | TBD | Unknown | |
| Linux | TBD | Unknown | |
| iOS | TBD | Unknown | |
| Android | TBD | Unknown | |
| Web browsers | TBD | Unknown | |

## Screen / Device Coverage

| Class | Required? | Status | Notes |
|---|---:|---|---|
| Mobile | TBD | Unknown | |
| Tablet | TBD | Unknown | |
| Laptop | TBD | Unknown | |
| Desktop | TBD | Unknown | |
| Ultrawide / high DPI | TBD | Unknown | |

## Browser Coverage

| Browser | Required? | Status | Notes |
|---|---:|---|---|
| Chrome / Chromium | Yes | Verified | Headless Edge, 2026-09-11 (`docs/index.html` v0.3.2), 7 widths (1600–360px). |
| Edge | Yes | Verified | Same pass as Chrome/Chromium above (Chromium-based). |
| Firefox | Yes | Verified | Playwright-driven real Firefox 155.0, 2026-09-12, `docs/index.html` at HEAD, 7 widths (1600–360px), both `prefers-reduced-motion: reduce` and default. Zero horizontal overflow, layout matches Chromium pass. |
| Safari | Yes | Verified (WebKit engine, not Apple Safari) | Playwright's bundled WebKit build used as a proxy — **not genuine Apple Safari**; does not cover Safari-specific quirks, its exact font rendering, or Apple's WebKit version. Same 7-width pass as Firefox above, zero horizontal overflow, layout matches Chromium/Firefox. A real Safari check on Apple hardware remains open. |

## Accessibility / Usability

- Keyboard navigation:
- Contrast:
- Screen reader basics:
- Reduced motion:
- Responsive layout:

## Notes

Mark unsupported platforms explicitly. Do not imply universal compatibility unless tested.
