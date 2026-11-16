# Validation Report — Redesigned Prototype

## v3 — review v2 changes (2026-11-15)
Applied [review_v2_changes_spec.md](review_v2_changes_spec.md). Re-verified independently: **73/73 interaction checks pass** (new checks: hero demo final state and Replay, computed years = 1.5, favicon, both demo thumbnails, print media). Overflow is 0 at 320/390/820/1440, there are no console errors, and the content sweep is clean. Heights (desktop/tablet/mobile): 10,009 / 11,490 / 14,574 px. Deviations: mobile H1 is 38px at ≤360px to avoid overflow; print forcing `<details>` open relies on Chromium `::details-content` plus a `beforeprint` handler (only tested with emulated print media). The items in the spec's "Skipped" table are not done; they need the owner's input.

## v2 — clarity changes (2026-11-15)
Applied [clarity_changes_spec.md](clarity_changes_spec.md), which comes from [portfolio_clarity_review.md](portfolio_clarity_review.md).

| Check | Result |
|---|---|
| Interaction suite (updated for v2: demos start inside closed details, new nav, no canvas, no raw email in hero, pip copy) | **51/51 passed**, re-run independently |
| Page overflow at 320 / 390 / 820 / 1440 (also with all details open) | **0** everywhere |
| Console errors | none |
| Page height (desktop / tablet / mobile) | 7,995 / 9,346 / 11,911 px (v1: 9,514 / 12,632 / 16,960) |
| Content sweep (Hire Me, resume/PDF, avatar, phone, old email, invented metrics, canvas, open-to status, inline styles) | no matches |
| Visual review | desktop light and dark plus mobile: single left edge, no orphan cards, standard project cards consistent |

**Deviations, accepted:** the demo tabs, the case-study marker, the active stepper step and the lit pipeline stage keep the accent, because they are actions or state, not decoration. No OG image yet. Cert years, verify links, reply time and open-to status are left out by the owner's decision.

---

## v1 (2026-11-14)

> Subject: `ux/prototype.html` (rebuilt). Validated 2026-11-14 in headless Microsoft Edge (Chromium) through `playwright-core` 1.48.
> Test scripts live in the session scratchpad and are not committed. They are reproducible with any Playwright setup.

## Commands
| Purpose | Command |
|---|---|
| Open | `file:///C:/workspace2/portfolio/ux/prototype.html` (no build, no server) |
| Full-page screenshots + overflow + console errors at 1440 / 820 / 390 | `node shoot.js <url> <outPrefix>` |
| Interaction suite | `node test.js` |
| Dark-mode captures | `node dark.js <url> <outPrefix>` |

## Results

### Layout
| Viewport | Height | Page-level horizontal overflow | Console errors |
|---|---|---|---|
| 1440 | 9,514 px | **0** (was 0) | none |
| 820 | 12,632 px | **0** (was 191) | none |
| 390 | 16,960 px | **0** (was 78) | none |
| 320 | — | **0** | none |

### Interaction suite: 36/36 passed (final run, after the fixes below)
- Playground: a preset returns 3 results with the term marked; the chunk-size slider changes the chunk count (8 → 16); overlap is clamped below size; config and tests queries return relevant chunks; zero-score state; empty-query hint; a query containing `<img onerror>` injects no element.
- Agent Registry tabs: arrow keys move to Promotion, Home returns to the diff tab; switching the diff sample recomputes the counts (+2 ~3 −1 → +1 ~4 −1).
- Promotion stepper: reaches the final message; the badge text stays identical; the badge moves from the Lower to the Higher lane; Next is disabled at the end; Reset works.
- Theme toggle; scroll-spy `aria-current`; progress bar; nav indicator; copy-email toast with the check state; canvas renders.
- Mobile menu: hidden initially, opens, Esc closes and returns focus, a link click closes it.
- `prefers-reduced-motion`: nothing left hidden, canvas draws a single frame, eyebrow shows full text. No-JS: all content visible.

### Visual review (screenshots inspected)
- Desktop, light and dark: every section header and its content share one left edge; there are no orphan cards; card footers line up.
- Mobile 390: header fits (logo, theme, menu); hero, pipeline card, proof strip and cards stack cleanly.

### Content review
- Grep sweep for removed or forbidden content (Hire Me, resume/PDF/download, avatar, phone, old email, invented metrics, non-resume skills, vendor model names, inline `style=`): **no matches** beyond false positives ("GenAI Engineer" in the title, CSS `50%`).
- The email matches the resume (`bpraveenkumar200321@gmail.com`). The title is Associate Engineer.

## Issues found during validation and fixed
| Issue | Fix |
|---|---|
| The sliding nav underline rendered under the logo, not the active link, because the desktop `.nav` rule set `position: static` | Changed to `position: relative` |
| The playground opened with an empty right column | Pre-loads the first example query |
| Section spacing felt oversized (up to 112 px + borders) | `--sec` reduced to `clamp(56px, 7vw, 88px)` |

## Not verified / limitations
- Only Chromium (Edge) was tested. Firefox and Safari were not tested (`backdrop-filter`, `clip-path` reveal and canvas should work, but this is unconfirmed).
- No real-device touch testing. Pointer effects are disabled where `hover: none`.
- No screen-reader session (NVDA/VoiceOver). ARIA patterns were checked by test and by reading the code only.
- Motion frame rate was not measured. Animations use transform/opacity/clip-path, plus `stroke-dashoffset` for icon drawing.
- Contrast tokens were chosen for ≥4.5:1 but not measured with a tool on every state.
- No WCAG 2.2 AA conformance is claimed.
- Google Fonts needs network access. System fallbacks apply offline.
- Confidentiality: the owner should confirm employer/client policy before publishing the Agent Registry details ([ux_audit_report.md §5](ux_audit_report.md#5-confidentiality-note-for-the-owner)).
