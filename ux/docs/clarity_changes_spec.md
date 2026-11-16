# Clarity Changes — v2 Build Spec

> Source: [portfolio_clarity_review.md](portfolio_clarity_review.md). Owner decisions (2026-11-14):
> **Motion:** middle path. **Open-to status:** not shown. **Skills:** Strong / Working knowledge (list below). **Cert years, verify links, reply time:** left out (no data, nothing invented).
> This spec overrides [redesign_strategy.md](redesign_strategy.md) §2, §5, §8 where they conflict. Everything else (tokens, accessibility, responsive rules, the no-resume/no-Hire-Me/no-form/no-phone rules) still applies.

## Review items → decision

| Review item | Decision |
|---|---|
| Plain one-liner + quick facts in hero | Done (below). Uses "Since March 2025" instead of "1.7 years" so it never goes stale |
| "Open to" status | **Not shown** (owner) |
| Hero photo | No photo available. Hero right becomes a plain-language "What I can help with" card |
| One "Email me" button in hero; footer email as icon | Done |
| Contact: why to write, reply time | Why to write: done. Reply time: **left out** (owner) |
| Nav: About · Experience · Projects · Open source · Skills · Contact | Done; "RAG" label dropped |
| RAG deep dive moves into the Enterprise RAG project | Done (inside its Technical details) |
| Standard project card for every project | Done |
| Open source section | Done. Downloads/stars **not shown** (no verified data) |
| Plain sentence at the top of every section | Done |
| Technical depth behind "Technical details" expanders | Done |
| Remove repetition (RAG ×6, AI tools ×4, duplicate agent-config tags) | Done (see "say it once" map) |
| Tags ≤ 5 per card | Done |
| Skills Strong / Working (~20) | Done (owner-approved list) |
| Cert years + verification links | **Left out** (owner) |
| Accent only for actions + one key line per section | Done |
| Remove canvas, typing, tilt, magnetic button | Done (middle path keeps reveals, progress bar, demos, timeline) |
| Eyebrows 13–14px sentence case | Done |
| aria-label on split-word text | Replace with visually-hidden text + `aria-hidden` word spans |
| Raw email wraps on phones | Button instead of raw address in hero and footer; contact address wraps safely |
| Freelance "2022 – Present" overlap | **Kept as on the resume** (title and dates are resume facts); the entry now leads with plain outcomes |
| OG image | Not created (no photo/brand asset). Left as an open item |
| Resume download | Stays removed (owner's earlier instruction). LinkedIn is the visible alternative in the hero |

## "Say it once" map
| Topic | Where it is explained in depth | Elsewhere only |
|---|---|---|
| RAG | Enterprise RAG project → Technical details (pipeline, decisions, playground) | Hero help card item 2, About "at a glance" item 1, Experience outcome 1 |
| AI coding tools (Claude Code, Devin, Antigravity) | Hero help card item 3 (engineer line) | Skills (Strong / Working) only |
| Agent configuration (skills, subagents, rules…) | How I work | Nowhere else |
| unified-file-reader | Open source section | Experience outcome (one line), About item 3 |

---

## New page order & nav

```
Header:  Praveenkumar   About  Experience  Projects  Open source  Skills  Contact   [theme] [menu<900]
1 Hero                (#top)
2 About               (#about)        plain bio + "At a glance" (4 items, the former proof strip)
3 Experience          (#experience)
4 Projects            (#projects)     Agent Registry · Enterprise RAG · Unified ML Framework · Attendance system
5 Open source         (#open-source)
6 Skills              (#skills)
7 How I work          (#approach)     not in nav
8 Education & certifications (#credentials) not in nav
9 Contact             (#contact)
Footer
```

## Visual rules (changes only)
- **Eyebrows:** 13px (14px ≥900px), sentence case, Inter 600, color `--text-2`, letter-spacing .01em. Not mono, not uppercase, not accent.
- **Accent (`--accent`) only on:** buttons, links, focus rings, scroll-progress bar, nav underline, and **one key line per section** (the hero headline; elsewhere the section's plain-language lead sentence may use `--text`, not accent). Tags, timeline markers, step numbers and card labels become neutral (`--text-2` / `--border`).
- **Tags:** max 5 per card.
- **Plain lead sentence:** every section starts (under the H2) with one everyday sentence in `.lead` (18px, `--text`). Technical text below it in `--text-2`.
- **Expander pattern:** `<details class="tech">` with summary "Technical details" (Agent Registry and RAG summaries: "Technical details & live demo"), a chevron that rotates, and content that fades/slides open (CSS only; reduced-motion = instant).

## Motion (middle path)
**Remove:** hero particle canvas (keep the static faint dot grid), the typing eyebrow, word-by-word / letter mask reveals (headings now reveal as one line: a 12px rise + fade, or one clip-path wipe of the whole line), 3D tilt, magnetic buttons, every count-up (step numbers, diff chip counts).
**Keep:** a short load sequence (header, then hero blocks fading up in order, ≤900ms total); scroll reveals (rise + fade, staggered children, once); scroll-progress bar; sliding nav underline; subtle cursor spotlight on cards (hover devices only); timeline line growth; the RAG pipeline visual with travelling packet (now inside the RAG project details, started when visible); playground FLIP re-flow and score bars; diff line reveal (faster: 20ms per line, once per sample switch); promotion stepper badge movement; How I work connector draw.
`prefers-reduced-motion: reduce` → everything static and visible, as before.

---

## Exact copy

### Head
- `<title>` `Bathala Praveenkumar — Backend & AI Engineer`
- meta description: `Backend & AI engineer at Covasant in Hyderabad. I build the software behind AI products: APIs, AI search over company documents (RAG), and safe release of AI assistants. Python, FastAPI, LangChain.`
- og:title / og:description mirror the above.

### Header
- Brand text: `Praveenkumar` (with "BP" monogram if already styled).
- Nav links: `About` #about · `Experience` #experience · `Projects` #projects · `Open source` #open-source · `Skills` #skills · `Contact` #contact.

### 1. Hero
- Eyebrow: `Backend & AI Engineer · Hyderabad, India`
- H1: `Bathala Praveenkumar`
- Headline (the hero's accent line): `I design, build and scale the software behind AI products.`
- Plain lead: `In plain words: I build the systems that let AI assistants answer questions from a company's own documents, and the backends that release those assistants safely to many customers.`
- Second line (text-2): `I use AI coding agents with a spec-first process to ship clean, modular code faster.`
- Quick facts (row of neutral chips with small icons): `Associate Engineer at Covasant` · `Since March 2025` · `Python & FastAPI` · `Hyderabad, India`
- Buttons: primary `View projects` → #projects; ghost `Email me` → `mailto:bpraveenkumar200321@gmail.com` (envelope icon).
- Icon links with visible labels: `LinkedIn` https://www.linkedin.com/in/bathala-praveenkumar · `GitHub` https://github.com/praveen9392. **No raw email address in the hero.**
- Right card — title `What I can help with`. Three items, each: plain title (600), plain sentence (text), engineer line (mono 12–13px, text-2, prefixed "For engineers:" visually hidden or shown as a small label):
  1. `Reliable backend APIs` — `Fast, well-tested services that apps and AI features run on.` — `FastAPI · Pydantic · SQLAlchemy · PostgreSQL`
  2. `AI that answers from your documents` — `Assistants that find the right passage first, then answer.` — `RAG · LangChain · FAISS · ChromaDB`
  3. `Faster delivery with AI coding agents` — `A spec-first process that keeps AI-written code clean and reviewed.` — `Claude Code · Devin · Google Antigravity`
  - Card footer link: `See my projects ↓` → #projects

### 2. About (#about)
- Eyebrow `About` · H2 `Backend engineer for AI products`
- Lead: `I work on the part of AI products that users never see: the services that store and find information, connect to AI models, and roll out updates safely.`
- Body (text-2): `I'm an Associate Engineer at Covasant in Hyderabad. Since joining in March 2025 I've worked across several parts of the AI stack: document search for AI assistants, a platform for releasing AI agents, and a framework for machine-learning projects. I care about code that is clean, tested and easy for the next person to change.`
- Sub-heading `At a glance` — 4 items (icon + bold plain label + small technical line):
  1. `Built AI search over company documents` — `Retrieval-augmented generation (RAG)`
  2. `Built the backend that releases AI assistants safely` — `Versioning, change previews, staged release, rollback`
  3. `Published an open-source Python library` — `unified-file-reader on PyPI`
  4. `Google-certified machine learning engineer` — `Professional Machine Learning Engineer`

### 3. Experience (#experience)
- Eyebrow `Experience` · H2 `Where I've worked`
- Lead: `One full-time role, plus freelance and open-source work alongside it.`
- **Associate Engineer — Covasant** · `Mar 2025 – Present` · `Hyderabad`
  - Intro: `Joined as an Associate Engineer and have worked across several parts of the company's AI platform.`
  - Outcome bullets (plain):
    - `Built AI systems that answer questions using a company's own documents.`
    - `Built backend features that let a platform release, upgrade and roll back AI assistants safely for many customers.`
    - `Built a framework where a new machine-learning use case starts with a config change instead of new code.`
  - `<details class="tech">` Technical details: the four grouped bullets from v1 (RAG & GenAI / Agent platform / ML framework / Engineering), unchanged text. Tags (5): Python, FastAPI, PostgreSQL, LangChain, Google ADK.
- **Freelance Software Developer & Open-Source Contributor — Independent** · `2022 – Present`
  - Outcome bullets:
    - `Published a free Python library that reads many file types through one simple interface.`
    - `Contributed to a system that records attendance automatically from video.`
  - Technical details: `Developed and published the unified-file-reader package on PyPI.` · `Contribute to open-source projects and reusable software tools.` · `Contributed to an Intelligent Video-Based Attendance System using Python, deep learning and OpenCV.`

### 4. Projects (#projects)
- Eyebrow `Projects` · H2 `Selected work`
- Lead: `Each project shows the problem, my part, and the result. Open "Technical details" for the engineering depth and live demos.`

**Standard card** (same markup for all): label row (category · context) → H3 title → one-line summary → definition list with `Problem` / `My role` / `Result` → tags (≤5) → links row → `<details class="tech">`.

**4.1 Agent Registry** — label `Team project · Covasant` — full width
- Title `Agent Registry`
- Summary: `A control panel to safely release and update AI assistants for many customers.`
- Problem: `Several customers can share one AI assistant, so upgrading it or undoing a bad release could affect all of them — and newer changes must never be lost.`
- My role: `Built backend features for versioning, change previews, staged release (test first, then live), upgrades across all customers, and rollback — in a multi-engineer team.`
- Result: `Merged into the shared codebase with unit tests. Every release is checked in a test environment before it goes live.`
- Tags: Python, FastAPI, SQLAlchemy, PostgreSQL, pytest
- Links row: button-link `Try the live demo` (opens this card's details and scrolls to the demo tabs).
- Details summary `Technical details & live demo` → contains, in order: v1 "What I built" list (unchanged text), the `Version diff | Promotion` tabs (unchanged behaviour, diff counts no longer count up), then the nested `<details>` "Read the case study" (unchanged text).

**4.2 Enterprise RAG system** — label `AI · Covasant` — full width
- Title `Enterprise RAG system`
- Summary: `AI search that answers questions using a company's own documents.`
- Problem: `General AI chatbots don't know a company's documents, so their answers can be vague or made up.`
- My role: `Built the full pipeline: reading documents, splitting them into passages, indexing them, finding the best matches for a question, and giving those to the AI model to answer.`
- Result: `Compared a LangChain build with a custom Python build, and tuned passage size and overlap for better matches.`
- Tags: Python, LangChain, FAISS, ChromaDB
- Links row: button-link `Try the live demo` (opens details, scrolls to playground).
- Details summary `Technical details & live demo` → contains:
  1. Short explainer: `RAG (retrieval-augmented generation) means the system first retrieves the most relevant passages from your documents, then asks the AI model to answer using only those passages.`
  2. The **animated RAG pipeline visual** (moved from the hero: 6 stages Documents → Parse → Chunk → Embed → Retrieve → Grounded answer, travelling packet, starts when visible).
  3. The 6 stage descriptions from v1 (Parse … Generate), compact list or grid, step numbers neutral, no count-up.
  4. "What I compared and tuned" (v1 text).
  5. Playground, heading `Try it: how the AI finds the right passage`, with the plain line first: `This shows how an AI assistant finds the right paragraph before answering. Change the passage size and watch the best matches change.` and the existing technical caption second (TF-IDF note). Behaviour unchanged; still pre-loads the first example.
  - Note: the playground must initialise correctly even though it starts inside a closed `<details>` (run on load and re-run/re-measure on `toggle`; FLIP must not break when hidden).

**4.3 Unified ML Framework** — label `ML · Covasant` — half width (pairs with 4.4 on ≥900px)
- Summary: `A framework that trains and deploys machine-learning models from a config file.`
- Problem: `Every new ML use case meant rewriting the same data preparation, training and evaluation code.`
- My role: `Designed and built a config-driven framework for supervised and unsupervised models.`
- Result: `New use cases need only a datasource and config update, with no code changes, which cut duplicated code.`
- Tags: Python, FastAPI, scikit-learn
- Details: `Automates preprocessing, model selection, training, evaluation and deployment.` · `Built on clean architecture principles.`

**4.4 Intelligent video-based attendance system** — label `Team project · Freelance` — half width
- Summary: `A system that records attendance automatically from video.`
- Problem: `Taking attendance by hand is slow and easy to get wrong.`
- My role: `Contributed to development using Python, deep learning and OpenCV.`
- Result: `Built as a team project; no public metrics.`
- Tags: Python, Deep learning, OpenCV
- Details: `Video-based recognition pipeline built with Python, deep learning models and OpenCV.`

### 5. Open source (#open-source)
- Eyebrow `Open source` · H2 `Code anyone can use`
- Lead: `A library I wrote and published so other developers can use it for free.`
- **unified-file-reader** card (standard card fields):
  - Summary: `A Python library that reads CSV, JSON, TXT, Excel, PDF, DOCX and more through one simple interface.`
  - Problem: `Every file type needs a different library and returns data in a different shape.`
  - My role: `Author: designed and published it, with a modular, strongly typed structure so new formats can plug in.`
  - Result: `Published on PyPI and GitHub for anyone to install.`
  - Install row: code `pip install unified-file-reader` + `Copy` button (toast "Install command copied").
  - Tags: Python, Typing, Packaging
  - Links: `GitHub` https://github.com/praveen9392/unified-file-reader · `PyPI` https://pypi.org/project/unified-file-reader/
- Below the card, one line: `I also contribute to open-source projects and reusable tools.` + link `See my GitHub →` https://github.com/praveen9392

### 6. Skills (#skills)
- Eyebrow `Skills` · H2 `Toolbox`
- Lead: `The tools I use every day, and the ones I know well enough to work with.`
- Two groups (label left, pills right; stacked on mobile):
  - `Strong`: Python, FastAPI, Pydantic, SQLAlchemy, PostgreSQL, REST APIs, RAG, LangChain, FAISS, ChromaDB, Google ADK, Claude Code
  - `Working knowledge`: Java, SQL, SQLite, Docker, NLP, Model training & evaluation, Devin, Google Antigravity

### 7. How I work (#approach)
- Eyebrow `How I work` · H2 `Spec first, agents second, review always`
- Lead: `AI writes code with me; a written plan and a careful review keep it clean.`
- 5 steps (one short line each):
  1. `Spec` — `Write what it must do and how we'll know it works.`
  2. `Plan` — `An agent drafts the plan; I own the structure and data contracts.`
  3. `Build` — `Agents implement small modules; subagents take parallel tasks.`
  4. `Verify` — `Linting, unit and regression tests, then a human review.`
  5. `Ship` — `Small changes that are easy to roll back.`
- Panel `How I set up AI agents`: Custom skills · Subagents · Reusable workflows · Global & workspace rules · Context management · Token optimization · Prompt engineering
- **Remove** the separate "Tools" panel (tools are named in the hero card and Skills).
- Principles row (unchanged text): Design / Build / Scale.

### 8. Education & certifications (#credentials)
- Eyebrow `Education` · H2 `Education & certifications`
- Lead: `Computer science degree and two professional certifications.`
- Cards unchanged (no years on certs, no links).

### 9. Contact (#contact)
- Eyebrow `Contact` · H2 `Let's talk`
- Lead: `Happy to hear about backend and AI engineering roles, project work, or open-source collaboration.`
- Small list (3 items, text-2): `Full-time engineering roles` · `Freelance or project work` · `Open-source collaboration`
- Contact block: primary button `Email me` (mailto) · address shown at 18–20px (not 32px, no animated underline) with `Copy` button · `LinkedIn` · `GitHub`. Line: `Based in Hyderabad, India`.

### Footer
`© 2026 Bathala Praveenkumar` · icon links (Email, LinkedIn, GitHub) each with `aria-label` · `Back to top`.
