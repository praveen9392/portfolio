# Screen-by-Screen Audit — Portfolio Prototype (before redesign)

> Method: full-page renders at 1440 / 820 / 390 px (headless Edge). Each section was scrolled top to bottom, and its markup and handlers were read. Screenshots were taken in the session scratchpad and are not committed.
> Severity: **C** critical · **H** high · **M** medium · **L** low.

---

## 1. Header
**Observed:** logo "BP Praveenkumar.ai", 7 text links, a ghost "Resume ⤓" button and a filled "Hire Me" button. Sticky with a blur.

| Finding | Sev |
|---|---|
| At 820 px the nav links stay visible until 768 px, so links and both buttons overflow the viewport. This is the main cause of the **191 px horizontal scroll** on tablet. | C |
| At 390 px "Resume" and "Hire Me" are not hidden. They crowd the logo ("Praveenkumar.ai" touches the Resume button), and the ☰ button is pushed past the edge, adding to the 78 px overflow. | C |
| "Resume" downloads a deleted file (404). | C |
| "Hire Me" competes with three hero CTAs. Owner asked for it to be removed. | H |
| "Architecture Lab" in the nav points to a sub-block, not a section, so the scroll-spy never highlights it. | L |

## 2. Hero
**Observed (desktop):** a status pill ("Available for High-Impact AI Engineering Roles"), the H1 name, "AI Engineer | Python Backend Developer", a 4-line intro, 3 CTAs, a "CONNECT:" row, and on the right the avatar card.

| Finding | Sev |
|---|---|
| Three CTAs, plus two header buttons, give **5 competing actions** above the fold. "View Resume (PDF)" is a 404. | H |
| The `min-height: calc(100vh − 4.5rem)` with vertical centring leaves about 160 px of dead space above the content and about 200 px below it at 1440×900. | M |
| At 390 px the role line wraps into an orphan "AI Engineer \|" with the separator dangling, and the CTAs stack into three full rows. | M |
| "CONNECT:" row: the location wraps under the pin emoji at 390 px. Emoji icons are mixed with SVG icons. | L |
| The positioning reads "AI Engineer" generically. It doesn't lead with RAG/backend or say Associate Engineer. | H |

## 3. AI Digital Avatar widget
**Observed:** a cartoon SVG face, a speech bubble, "QUICK INQUIRIES (RECRUITER PRESETS)", 4 chips, a text input and Ask. A Voice (TTS) toggle is on by default.

| Finding | Sev |
|---|---|
| It is labelled "PORTFOLIO GROUNDED AGENT • v1.2", but it is a substring lookup over 8 canned answers. For a GenAI engineer, a visitor who notices this may lose trust in every other claim on the page. | C |
| Wrong answers: the **"RAG Pipelines" chip returns the Covasant answer**, and "ML framework" does too. | C |
| Canned answers contain invented facts (4-person team, 50%, 30%). | H |
| TTS is on by default and speaks on a chip click. That is unexpected audio and an accessibility concern. | M |
| At 390 px the speech bubble is ~130 px wide, so it shows 1–2 words per line across 11 lines. | M |
| The cartoon portrait is generic and reads as clip-art. | M |
| Owner explicitly dislikes it. | H |

## 4. Highlights strip
**Observed:** "100% Configuration-Driven Pipelines", "v1.0.0+ Semantic Versioning Deployments", "PyPI Published Package Creator", "Google ML Certified (2025)".

| Finding | Sev |
|---|---|
| These are labels dressed as metrics. "100%" and "v1.0.0+" don't measure anything, and experienced reviewers read that as padding. | H |
| The mobile background band stops ~80 px short of the right edge because of page overflow. | M |
| The cert year isn't in the resume. | M |

## 5. About
**Observed:** a 4-paragraph left column and 3 philosophy cards on the right.

| Finding | Sev |
|---|---|
| The left column is about 2× taller than the cards, leaving a large empty area on the right (desktop). | M |
| The copy is generic ("bridging the gap", "real-world loads"), and "zero ungrounded hallucinations" is an absolute claim that can't be backed. | M |
| No mention of AI-assisted development or spec-driven work, which the owner wants highlighted. | H |

## 6. Experience
**Observed:** a vertical timeline with 2 cards.

| Finding | Sev |
|---|---|
| **Misaligned:** the timeline wrapper is `max-width: 860px; margin: auto`. The rail sits at x≈315 and the cards at x≈362, while every section heading starts at x=124. This is the most visible alignment break on desktop. | H |
| The role says AI Engineer; the owner wants Associate Engineer and the "started here, worked across parts" story. | H |
| The bullets are a flat list. Grouping by area (RAG, platform, ML framework) would scan faster. | M |
| The freelance card contains invented claims (global clients, team lead, 50%). | H |

## 7. Skills
**Observed:** 5 filter pills and 5 cards in an `auto-fit minmax(280px)` grid.

| Finding | Sev |
|---|---|
| 4 cards on the first row, then **1 orphan card** on the second row (desktop). | H |
| Tag clouds have uneven lengths, so the cards have ragged bottoms. | L |
| Contains skills not on the resume, and is missing resume skills (AI coding tools, agent configuration, Ruff, code reviews, PostgreSQL). | H |
| `role="tab"` without `aria-selected`, `tabpanel` or arrow-key support. The filter adds little for about 45 tags. | M |

## 8. Projects
**Observed:** 5 cards in an `auto-fill minmax(360px)` grid, then the Architecture Lab panel.

| Finding | Sev |
|---|---|
| `minmax(360px, 1fr)` is wider than the 342 px content box at 390 px, so cards overflow (**part of the 78 px overflow**). | C |
| 3 + 2 layout leaves an empty third slot (desktop). | M |
| All 5 projects get equal weight; the flagship and RAG are not prioritised. | H |
| Card footers misalign: buttons sit at different heights because the content above has different lengths. Ghost buttons have inconsistent heights (GitHub Repo vs Details). | M |
| The modal has no focus management and uses inline styles. | M |
| "Benchmarked … sub-50ms" and "Reduced … 50%" are unverified. | H |

## 9. Architecture Lab
| Finding | Sev |
|---|---|
| A good idea, and the strongest proof element on the page, but it is buried under the project grid. | M |
| Counts are hard-coded and **wrong for sample 2**. | H |
| "Experience the exact version-diff logic Praveen designed" overstates a static, hand-written sample. | M |
| "Simulate Batch Promotion" only fires two toasts; nothing in the panel changes. | M |
| Uses real vendor names (gemini, cohere, stripe) in fake configs. | M |

## 10. Resume & Academic Background
| Finding | Sev |
|---|---|
| The "Verified Resume Document" hub has 2 dead links, a fake "DOCUMENT SIGNATURE", and "PAGES: 3" (the resume is 2). | C |
| Owner asked for no download options. | H |
| The education/certifications content is useful and should be kept in compact form. | — |

## 11. Contact
| Finding | Sev |
|---|---|
| **The form fakes success** and loses the message. A recruiter who uses it believes they reached him. | C |
| The email differs from the resume. | H |
| The info column (top 715) and form card (top 691) don't share a top edge. | L |
| The name is interpolated into `innerHTML` (self-XSS pattern). | M |

## 12. Footer
| Finding | Sev |
|---|---|
| Fine, but it repeats the same 3 links; no copyright line. | L |

## Cross-cutting
- **Contrast:** `--text-muted #64748b` on `#090d16` is about 3.9:1 (calculated). It is used for 12–13 px labels, which fails WCAG 1.4.3 (4.5:1).
- **Inline styles:** more than 60 `style=""` attributes, which undermines the design tokens.
- **Skip link:** implemented with inline `onfocus`/`onblur` style swaps. It works but is brittle.
- **Motion:** only the hero pulse and the modal/toast animations. Sections appear with no choreography, so the page feels static compared with the "world-class" goal.
