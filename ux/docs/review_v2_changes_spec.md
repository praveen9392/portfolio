# Review v2 — Change Spec (v3 build)

> Source: [portfolio_clarity_review.md](portfolio_clarity_review.md) (Review v2, 2026-11-15). Overrides [clarity_changes_spec.md](clarity_changes_spec.md) where they conflict. All earlier hard rules stay: no Hire Me, no resume/PDF, no form, no phone, no invented facts. Keep a11y, reduced-motion and no-JS behaviour, zero overflow at 320/390/820/1440, and no console errors.

## Skipped review items (need owner input or data we don't have)
| Item | Why skipped |
|---|---|
| Photo, `og:image` share card | No photo/asset supplied |
| Availability badge ("Open to…") | Owner decided on 2026-11-14 not to show a status |
| Cert years / verify links / badge image; dropping the Microsoft course | Owner: leave out; the course is on the resume |
| Response-time promise, "Book a 15-min call" | Owner: no reply time; no booking link exists |
| Testimonials, client logos | None supplied |
| Business-impact numbers (time saved etc.) | None in the resume; results rewritten impact-first, qualitatively |
| Downloads / tests-passing badges | Unverified; only the live PyPI version + Python-versions badges are used |
| "Download one-page summary" | Owner banned resume/download links; the print stylesheet makes the page itself printable |

## Changes to make

### Colour system (replaces the "neutralise accent" layer — remove those overrides)
Tokens for both themes:

| Token | Dark | Light | Use |
|---|---|---|---|
| `--accent` (teal) | `#5eead4` | `#0f766e` | buttons, links, focus, progress bar, nav underline/current item |
| `--c-backend` (blue) | `#60a5fa` | `#1d4ed8` | Backend theme |
| `--c-ai` (violet) | `#a78bfa` | `#6d28d9` | AI / RAG theme |
| `--c-delivery` (amber) | `#fbbf24` | `#b45309` | AI-assisted delivery, How I work, certificates, key numbers |
| `--c-status` (green) | `#4ade80` | `#15803d` | success toasts, diff "added" |

Rules: category colours never on buttons. At most one coloured element per card besides the label (top border 3px **or** icon tile). Tags stay neutral; the card's category label is coloured. Tints = the hue at 10–12% alpha. Theme mapping: Agent Registry + ML Framework = backend; Enterprise RAG + playground = ai; How I work + certificates + stats numbers = delivery. Step numbers, timeline markers and principle labels take their section's colour.

### Typography & rhythm
H1 clamp(44px, 7vw, 72px), weight 800, tracking −0.03em. H2 clamp(32px, 4.5vw, 48px), weight 750–800. Leads 19–20px. `--sec: clamp(72px, 10vw, 128px)`. **Alternate section backgrounds** `--bg` / `--surface` in page order. Plain-language section leads get a soft marker highlight (background gradient underline in the section colour at ~18% alpha on the lead's key phrase, or the whole lead line) — subtle.

### Header
Monogram tile "BP" (teal-on-tint) + "Praveenkumar". Small ghost button `Email me` (mailto) at the right before the theme toggle (hidden <640px; it is in the mobile menu instead). Add an SVG favicon (data URI, "BP" on teal).

### Hero
- Eyebrow: `Backend & AI Engineer · Hyderabad, India`
- H1: `Bathala Praveenkumar`
- Headline (plain sentence now leads; gradient teal→violet on the words `answer from a company's own documents`, one 1.2s gradient sweep on load, then static): `I build the systems that let AI assistants answer from a company's own documents — and release them safely.`
- Sub-line: `I design, build and scale backend software for AI products, with clean, modular, tested code.`
- **Remove** the "In plain words:" paragraph and the AI-coding-agents sub-line (that idea lives in How I work).
- Facts chips (3): `Associate Engineer at Covasant` · `{N}+ years building AI backends` · `Hyderabad, India`. `{N}` is computed in JS from 2025-03-01 to today, floored to 0.5 (e.g. 1.5); no-JS fallback text `Building AI backends since March 2025`.
- CTAs: primary `View projects →` (arrow nudges 3px on hover), ghost `Email me`. Links: LinkedIn, GitHub.
- **Right column: signature "Ask → Find → Answer" card** (violet theme), labelled `How AI search works` with a tiny `Illustration` tag:
  1. A search box types the question `How do refunds work?` (typing allowed here: it is inside the demo card, not a heading).
  2. Three document cards slide in (`Policy.pdf`, `FAQ.md`, `Orders.csv`); `Policy.pdf` lights up violet with the sentence `Refunds are issued to the original payment method within 5 business days.` highlighted.
  3. An answer bubble: `Refunds go back to your original payment method within 5 business days.` + chip `Source: Policy.pdf, p.3`.
  - Plays once on load (~4s total; first paint shows the card frame instantly), then a `Replay` button. Pause and reset when off-screen. Reduced motion: shows the final state statically. `aria-live` is off for the animation; give the card a visually-hidden text summary of all three steps.
- On phones: copy and CTAs come before the card (already the case).

### "What I can help with" → three coloured tiles directly below the hero
A section strip (no H2 needed, or a small eyebrow `What I can help with`), 3 tiles in a row (stacked on mobile). Each: icon tile in its colour, plain title, plain sentence, engineer line (same copy as v2): backend (blue), AI (violet), delivery (amber).

### Stats band (under the tiles)
4 large numbers (48–64px, `--c-delivery` or teal→violet gradient text), count up once over 800ms when 50% visible; reduced motion = final values:
- `{N}+` — `years building AI backends at Covasant` (same computed N)
- `6` — `stage RAG pipeline, from parsing to grounded answers`
- `6+` — `file formats read through one API (unified-file-reader)`
- `1` — `Google Professional ML Engineer certification`

### About → short story (remove "At a glance"; the stats band replaces it)
- Eyebrow `About` · H2 `From open-source tools to AI platforms`
- Lead: `I like turning messy problems into small, clear pieces of software that other people can build on.`
- Body: `I studied Computer Science at Sreenivasa Institute of Technology and Management Studies (2020–2024). Alongside my degree I started freelancing and building open-source Python tools, and published unified-file-reader on PyPI. In March 2025 I joined Covasant as an Associate Engineer, where I've worked across several parts of the AI stack: document search for AI assistants, a platform for releasing AI agents, and a framework for machine-learning projects.`

### Experience
- Timeline line fills in teal as you scroll (scroll-linked, already exists — colour it); markers coloured.
- Rename the second entry title to `Side projects & open source` with the sub-line `Freelance software developer & open-source contributor · Independent` · `2022 – Present`. Bullets unchanged.

### Projects
- Card demo buttons become **secondary** (ghost) style, labelled `Open live demo`, with a small `Live demo` pill in the card's label row.
- **Demo thumbnail on the card** (right side ≥900px, below the summary on mobile): a small static CSS/SVG preview — Agent Registry: 4 mini diff lines (+/~/− coloured bars); RAG: a query bar with 3 ranked chunk bars. Clicking the thumbnail = same as the demo button (opens details, scrolls to demo). It is a `<button>` with an accessible name `Open live demo: …`.
- Hover: lift 4px + border glow in the category colour, 200ms. Card spotlight tinted by the category colour.
- **Results, impact first** (replace text):
  - Agent Registry: `Customers sharing an assistant can be upgraded together, and a bad release can be undone without losing newer changes. Merged into the shared codebase with unit tests.`
  - Enterprise RAG: `Answers come from the company's own documents instead of the model's guesses. Passage size and overlap were tuned for better matches, and a LangChain build was compared with a custom one.`
  - Unified ML Framework: `A new ML use case starts with a datasource and config update instead of new code, which cut duplicated code across projects.`
- **Architecture diagram** in the Agent Registry case study (inline SVG, theme-aware, labelled `Illustrative architecture`): `Agent version 1.1.0` → `Shared deployment (Tenant A · Tenant B · Tenant C)` → `Lower environment: deploy & validate` → `Higher environment: promote same batch`, with a dashed `Rollback` arrow back from Higher to the previous batch. Has a `<title>`/`<desc>` and a text alternative.
- Attendance system → **"Other work"** single-row item under the cards: `Other work — Intelligent video-based attendance system: contributed to a system that records attendance automatically from video (Python, deep learning, OpenCV).`

### Open source
Add two live badges under the title (`<img>` with alt text, height 20, lazy):
- `https://img.shields.io/pypi/v/unified-file-reader` alt `PyPI version`
- `https://img.shields.io/pypi/pyversions/unified-file-reader` alt `Supported Python versions`
If they fail to load, hide them (`onerror` handler set in JS, not an inline attribute).

### Skills
- `Strong` grouped by area, each with a small icon in its colour: `Backend` (blue): Python, FastAPI, Pydantic, SQLAlchemy, PostgreSQL, REST APIs · `AI` (violet): RAG, LangChain, FAISS, ChromaDB, Google ADK · `Tools` (amber): Claude Code
- `Working knowledge` (neutral): Java, SQL, SQLite, Docker, NLP, Model training & evaluation, Devin, Google Antigravity

### How I work (amber theme)
- Lead: `I use AI coding agents (Claude Code, Devin, Google Antigravity) every day. A written spec and a careful review keep the output clean.`
- Keep the 5 steps (numbers in amber).
- Replace the agent-setup tag cloud with a short definition list `How I set up AI agents`:
  - `Custom skills & reusable workflows` — `Repeatable instructions for tasks I do often, so agents follow the same steps every time.`
  - `Subagents` — `Separate agents for parallel tasks, each with a narrow job.`
  - `Global & workspace rules` — `Project conventions written down once, so generated code matches the codebase.`
  - `Context management & token optimization` — `Give the agent only the files and rules it needs, so its output stays focused and fast.`
- Principles row unchanged; labels in amber.

### Education & certifications
Certificate cards get an amber icon tile. Text unchanged.

### Contact
Unchanged copy. Email address row keeps Copy. (No call link, no reply time.)

### Motion additions (all once, transform/opacity/clip-path only, reduced-motion = static)
Hero card sequence; headline gradient sweep; stats count-up; button arrow nudge; card hover lift/glow; section headings reveal with a clip-path wipe up (500ms, whole line, not per word). Keep everything else from v2. No particle backgrounds, no heading typing, no cursor followers.

### Print stylesheet
`@media print`: white background, black text, hide header, nav, theme toggle, demos, buttons, thumbnails and the hero card; open all `<details>`; show link URLs after external links; avoid breaking inside cards.
