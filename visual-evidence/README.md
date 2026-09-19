### Motivation

The theme builder's popup and hex input are clipped by the docs theme's table overflow rule. Targeting `table.color-picker` lets its existing `overflow: visible` rule take precedence. Other tables keep their existing styles.

### Related issue

Fixes #5093.

### Screenshots / Videos

Local production docs build, v5, Chromium 153, 1280px:

| Before | After |
| --- | --- |
| ![Before](https://raw.githubusercontent.com/fatihcvs/react-native-paper/bf479d4d14ea913afefe70a0084591073d1fa31c/visual-evidence/paper-chromium-v5-1280-before-primary.png) | ![After](https://raw.githubusercontent.com/fatihcvs/react-native-paper/bf479d4d14ea913afefe70a0084591073d1fa31c/visual-evidence/paper-chromium-v5-1280-after-primary.png) |

v6, Firefox 151, 390px:

| Before | After |
| --- | --- |
| ![Before](https://raw.githubusercontent.com/fatihcvs/react-native-paper/bf479d4d14ea913afefe70a0084591073d1fa31c/visual-evidence/paper-firefox-v6-390-before-primary.png) | ![After](https://raw.githubusercontent.com/fatihcvs/react-native-paper/bf479d4d14ea913afefe70a0084591073d1fa31c/visual-evidence/paper-firefox-v6-390-after-primary.png) |

The before captures restore only the original `.color-picker` selector in the served CSS. [All viewport/browser comparisons and measurements](https://github.com/fatihcvs/react-native-paper/tree/bf479d4d14ea913afefe70a0084591073d1fa31c/visual-evidence) are on a separate evidence branch.

### Test plan

On v5 and v6, at 1280px and 390px, in Chromium 153 and Firefox 151:

- Open primary, secondary, tertiary, and custom color pickers.
- Confirm the entire popup and hex input are visible; enter `123456`, select a palette swatch, and dismiss by clicking the overlay.
- Check an ordinary table on the same page retains its width, display, and overflow.

All 32 post-fix picker cases passed; the original selector reproduced clipping in all 32 baseline cases. Fresh Windows validation on 2026-09-20 with Node 24.13.0 / Yarn 4.9.1: lint, typecheck, docs build, and 54 test suites passed (678 tests, 234 snapshots; 1 test skipped).

The existing Contributor Label workflow fails while creating its GitHub App token (`Invalid keyData`), before it evaluates this change.

AI-assisted patch and verification; no runtime logic or dependencies changed.
