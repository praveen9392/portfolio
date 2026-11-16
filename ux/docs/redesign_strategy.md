# Redesign Strategy & Content Specification

> Companion to [ux_audit_report.md](ux_audit_report.md). This file is the build contract for `ux/prototype.html`.
> Content rule: **every claim must trace to the resume (`Praveen (1).pdf`) or the sanitised Agent Registry analysis.** No invented metrics, no invented years, no employer/client names other than Covasant.

---

## 1. Positioning (what changes and why)

| Before | After | Why |
|---|---|---|
| "AI Engineer \| Python Backend Developer" | **Associate Engineer at Covasant** — Python backend engineer for GenAI | Owner's instruction; accurate title builds trust. Breadth is told as "started as Associate Engineer, worked across different parts of the stack". |
| Generalist list of 5 equal projects | **RAG first**, then Agent Registry backend, then supporting work | Owner wants RAG as the headline; research says lead with 2–3 strong, deep pieces. |
| AI "digital avatar" chatbot (keyword matcher + TTS) | Animated **RAG pipeline diagram** in hero + real in-browser **chunking & retrieval playground** | The avatar was a keyword `includes()` lookup presented as an "AI agent" — a credibility risk for a GenAI engineer. A working, honestly-labelled retrieval demo proves understanding instead. |
| "Hire Me", "Resume" download, "View Resume (PDF)", Resume hub section | **Removed entirely.** Single CTA family: "See the RAG work" / "Get in touch" | Owner's instruction. Also removes a broken link (`Praveen.pdf` is no longer in the repo — commit `0c68c1a`). |
| Simulated contact form that pretends to send | Direct email (with copy button), LinkedIn, GitHub | A form with no backend that shows "sent" is a false success state. |
| Skills include items not on the resume (Java Spring Boot, Hibernate, caching, task queues, CI/CD, monitoring, face recognition, fine-tuning) | **Only resume skills**, grouped as on the resume | Owner's instruction; interview-safe. |
| Made-up numbers (sub-50ms, 50% effort cut, 30% accuracy, "4-person team lead", "100%", "v1.0.0+", "3 pages", cert years) | Removed | Not in resume; unverifiable claims are a red flag. |
| New: — | **"How I build"** section: spec-driven development with Claude Code, Devin, Google Antigravity; skills, subagents, rules, context & token management | Owner wants AI-tool adoption highlighted; it is a differentiator in 2026. |
| New: — | **Design → Build → Scale** principles | Owner: "I can design, build, scale efficiently". |

## 2. Information architecture

Single page, 8 sections, one nav:

```
Header:  BP Praveenkumar      Experience  RAG  Projects  How I build  Skills  Contact   [theme]
1. Hero            (#top)
2. Proof strip     (factual, no metrics)
3. What I do       (#about)       3 pillars: Backend · RAG & GenAI · AI-assisted engineering
4. Experience      (#experience)
5. RAG             (#rag)         pipeline + decisions + playground   ← featured
6. Projects        (#projects)    Agent Registry flagship (+ diff lab, promotion stepper) + 3 cards
7. How I build     (#approach)    spec-driven flow + agent config + Design/Build/Scale
8. Skills          (#skills)
9. Credentials     (#credentials) education + certifications (compact)
10. Contact        (#contact)
Footer
```

Nav has no buttons other than a theme toggle and (mobile) a menu button. No "Hire Me", no "Resume".

## 3. Visual direction — "Quiet technical, cinematic motion"

Editorial, engineering-grade layout: confidence through alignment and typography. The cinematic feel comes from purposeful motion (§5), not from decorative glow blobs.

- **Grid:** one container `max-width: 1120px`, side padding `clamp(16px, 4vw, 32px)`. **Every section header, card grid, and timeline starts on the same left edge.** No nested off-centre containers.
- **Section rhythm:** `padding-block: clamp(64px, 9vw, 112px)`; header block → content gap 40px.
- **Type:** Inter (400/500/600/700) for UI and body, JetBrains Mono (400/500) for code, labels, data. Scale: 12 / 14 / 16 / 18 / 20 / 24 / 32 / clamp(36px, 6vw, 60px). Body 16–17px, line-height 1.65, measure ≤ 68ch.
- **Colour tokens (dark default, light supported):**

| Token | Dark | Light |
|---|---|---|
| `--bg` | `#0b0f17` | `#f7f8fa` |
| `--surface` | `#111723` | `#ffffff` |
| `--surface-2` | `#172031` | `#f0f2f6` |
| `--border` | `rgba(255,255,255,.08)` | `#e3e7ee` |
| `--text` | `#e8ecf3` | `#0f172a` |
| `--text-2` | `#a3adbf` | `#475569` |
| `--text-3` | `#8590a3` (≥4.5:1 on bg) | `#5b6577` |
| `--accent` | `#5eead4` (teal) | `#0f766e` |
| `--accent-ink` (text on accent) | `#04211d` | `#ffffff` |
| `--add` / `--mod` / `--del` | `#4ade80` / `#fbbf24` / `#f87171` | `#15803d` / `#a16207` / `#b91c1c` |

  One accent only. Diff colours are semantic only. No ambient blobs; at most a very faint dot-grid behind the hero.
- **Radii:** 8 (controls) / 12 (cards) / 999 (pills). **Shadows:** almost none; borders carry structure.
- **Icons:** inline SVG, 1.75 stroke, 20px, `currentColor`, always `aria-hidden` with text label.
- **Theme:** respects `prefers-color-scheme`; toggle sets `data-theme` on `<html>`; choice saved in `localStorage` inside try/catch.

## 4. Components

Button (primary / ghost, 44px min height), text link, pill/tag, card, section header (eyebrow mono label + H2 + one-line lede), timeline item, pipeline stage, segmented control (tabs with `role="tablist"` + arrow keys), range slider with visible value, code/diff block, stepper, disclosure (`<details>` for case-study depth instead of modal), toast (copy confirmation), skip link.

**Modals removed:** project depth moves into inline `<details>` disclosures — no focus-trap bugs, works without JS, better on mobile.

## 5. Motion — "every section should be felt" (owner requirement, 2026-11-14)

Stunning but purposeful: each animation explains or rewards something. GPU-only properties (transform, opacity, clip-path, filter), `requestAnimationFrame`, canvases paused when off-screen or tab hidden. Easing `cubic-bezier(.2,.7,.2,1)` (enter) / `cubic-bezier(.7,0,.2,1)` (move).

| Where | Animation |
|---|---|
| Page load | Short choreographed intro (≤1.2s total): header fades down, eyebrow types in, H1 letters/words rise from a clip mask with stagger, headline words reveal one by one, CTAs and links fade up last. Never blocks interaction. |
| Hero background | Canvas "embedding field": slow drifting nodes that connect with faint lines when near each other; nodes near the pointer brighten and gently attract (semantic-search metaphor). Theme-aware colours, ~60 nodes desktop / ~25 mobile, DPR-capped at 2. |
| Hero RAG card | Stages draw in sequentially; a glowing packet travels Documents → Grounded answer on a loop; each stage lights as the packet passes; subtle 3D tilt toward pointer. |
| Global | Thin scroll-progress bar under header (accent). Scroll-spy underline slides between nav links. Cursor spotlight (radial gradient following pointer) on cards. Magnetic primary buttons (≤6px pull). |
| Section headers | Eyebrow slides in, H2 reveals through a clip mask word by word, lede fades up — once per section. |
| Proof strip | Items stagger in; icons draw their strokes (stroke-dashoffset). |
| What I do | Pillar cards rise with stagger; tags cascade in; hover lifts with spotlight. |
| Experience | Timeline line grows with scroll progress (scroll-linked scaleY); markers pop and pulse once as they enter; bullets stagger. |
| RAG | Pipeline connector line draws as the section scrolls into view; stage cards reveal in sequence with their number counting in; playground chunks re-flow with FLIP animation when size/overlap change; retrieved results slide into rank order; score bars fill. |
| Projects | Flagship card scales up from 0.98; diff lines appear one by one (typewriter cadence ~40ms/line) when the tab first becomes visible; summary counters count up; promotion stepper moves the `Batch 1.1.0` badge physically from Lower to Higher lane with a progress line fill. |
| How I build | 5-step flow connector draws left→right (top→bottom on mobile) with steps lighting in order; tool chips float in. |
| Skills | Groups reveal with stagger; pills cascade in per group; hover glow. |
| Credentials/Contact | Cards rise; email row has an animated underline; copy button morphs to a check icon. |

Rules: every scroll animation runs **once**; nothing loops except the hero canvas and pipeline packet (both pausable). Content is visible without JS (`.js` class gate). **`prefers-reduced-motion: reduce` disables all of it** — canvas renders one static frame, everything else appears in final state. Target 60fps on a mid-range laptop; no layout thrash (no animating width/height/top/left).

## 6. Responsive

Breakpoints: 640 / 900 / 1100. Mobile-first. Header collapses to a menu button below 900px with an accessible disclosure menu (Esc closes, focus returns). Cards 1-col < 640, 2-col ≥ 640, 3-col ≥ 1100 where used. Diff block scrolls horizontally **inside itself** only. **Zero page-level horizontal overflow at 320, 390, 820, 1440.**

## 7. Accessibility targets (WCAG 2.2 AA)

Landmarks, one H1, ordered headings, skip link, visible `:focus-visible` ring (2px accent + 2px offset), 44×44 targets, all interactive demo controls labelled, live regions for playground results and toasts (`aria-live="polite"`), sliders with `aria-valuetext`, tabs with full ARIA tab pattern, colour never the only signal in diffs (+ / ~ / − glyphs + labels).

---

## 8. Content specification (exact copy)

### 8.1 Head
- `<title>`: `Bathala Praveenkumar — Backend & GenAI Engineer`
- meta description: `Associate Engineer at Covasant building Python backends for GenAI: RAG pipelines, LLM agents and agent-platform APIs. FastAPI, LangChain, Google ADK, FAISS, ChromaDB.`
- Open Graph title/description mirroring the above.

### 8.2 Hero
- Eyebrow (mono): `Associate Engineer · Covasant · Hyderabad, India`
- H1: `Bathala Praveenkumar`
- Headline (large, 2 lines max on desktop): `I design, build and scale backend systems for GenAI.`
- Lede: `Python and FastAPI engineer focused on RAG pipelines, LLM agents and the platforms that ship them. I started at Covasant as an Associate Engineer and have worked across different parts of the AI stack — retrieval, agent platforms, an ML framework and the APIs that connect them.`
- Second line (smaller, text-2): `I write clean, modular code and use AI coding agents — Claude Code, Devin, Google Antigravity — with spec-driven development to ship faster without lowering the bar.`
- CTAs: primary `See the RAG work` → `#rag`; ghost `Get in touch` → `#contact`.
- Links row (icon + text): GitHub `https://github.com/praveen9392`, LinkedIn `https://www.linkedin.com/in/bathala-praveenkumar`, Email `mailto:bpraveenkumar200321@gmail.com`.
- Right column visual: **RAG pipeline card** titled `RAG pipeline` with 6 vertical stages (Documents → Parse → Chunk → Embed → Retrieve → Grounded answer), each with a one-word mono hint (`PDF · DOCX · CSV`, `size + overlap`, `embeddings`, `FAISS · ChromaDB`, `top-k`, `with sources`). Animated travelling dot. Footer of card: `How I think about retrieval ↓` link to `#rag`.

### 8.3 Proof strip (4 items, icon + bold label + short line; no numbers)
1. `RAG pipelines` — `Parsing to grounded answers · FAISS · ChromaDB · LangChain`
2. `Agent platform backend` — `Versioning, diffs, promotion and rollback across tenants`
3. `Open source on PyPI` — `unified-file-reader`
4. `Google certified` — `Professional ML Engineer`

### 8.4 What I do (#about)
- Eyebrow `What I do` · H2 `Backend engineering for AI products` · lede `Three things I bring to a team.`
- Pillar 1 — **Backend engineering**: `FastAPI services with Pydantic contracts and SQLAlchemy on PostgreSQL. Layered API → service → repository code, typed domain errors mapped to HTTP status codes, and business rules kept in small, testable modules.` Tags: FastAPI, Pydantic, SQLAlchemy, PostgreSQL, REST APIs.
- Pillar 2 — **RAG & GenAI**: `Retrieval pipelines from document parsing and chunking to embeddings, vector search and context-aware LLM responses. LLM agents built with Google ADK.` Tags: RAG, LangChain, Google ADK, FAISS, ChromaDB.
- Pillar 3 — **AI-assisted engineering**: `Spec-driven development with Claude Code, Devin and Google Antigravity — custom skills, subagents, workspace rules and careful context management, so agents produce code that passes review.` Tags: Claude Code, Devin, Antigravity, Spec-driven.

### 8.5 Experience (#experience)
- Eyebrow `Experience` · H2 `Where I've worked`
- **Associate Engineer — Covasant** · `Mar 2025 – Present` · `Hyderabad`
  - Intro: `Started as an Associate Engineer and have worked across several parts of the AI platform stack.`
  - Grouped bullets (group label in mono, then text):
    - `RAG & GenAI` — `Built RAG pipelines covering document parsing, chunking, embedding generation, vector retrieval (FAISS, ChromaDB) and context-aware LLM responses; built LLM-based agents with Google ADK.`
    - `Agent platform` — `Built backend features for an AI agent registry: semantic versioning, configuration version diffs, tenant-centric promotion from lower to higher environments, fleet-wide agent version changes and batch rollback.`
    - `ML framework` — `Built a configuration-driven ML framework where a new use case needs only datasource and config changes, not code.`
    - `Engineering` — `Clean architecture, unit and regression tests with every change, code reviews, and delivery with cross-functional teams.`
  - Tags: Python, FastAPI, SQLAlchemy, PostgreSQL, LangChain, Google ADK, FAISS, ChromaDB
- **Freelance Software Developer & Open-Source Contributor — Independent** · `2022 – Present`
  - `Developed and published the unified-file-reader Python package on PyPI.`
  - `Contribute to open-source projects and reusable software tools.`
  - `Contributed to an Intelligent Video-Based Attendance System using Python, deep learning and OpenCV.`

### 8.6 RAG (#rag) — featured
- Eyebrow `Featured · RAG` · H2 `Retrieval-Augmented Generation, end to end` · lede `RAG quality is decided long before the LLM call. Most of my work is in the stages that feed it.`
- **Pipeline (6 stage cards, numbered, horizontal on desktop / vertical on mobile):**
  1. `Parse` — `Turn PDFs, DOCX, CSV, JSON and text into clean text with metadata. Same problem I solved in unified-file-reader.`
  2. `Chunk` — `Split documents by size and overlap. Too small loses context; too large dilutes relevance. I tune both per corpus.`
  3. `Embed` — `Generate embeddings for every chunk and keep chunk ↔ source mapping for citations.`
  4. `Index` — `Store vectors in FAISS or ChromaDB depending on the deployment need.`
  5. `Retrieve` — `Top-k similarity search for the query; retrieval quality is measured, not assumed.`
  6. `Generate` — `Context-aware LLM response grounded in the retrieved chunks, with sources the user can check.`
- **Decisions panel** — title `What I compared and tuned` — 3 items:
  - `LangChain vs custom Python` — `Built the same pipeline both ways to see where the framework helps and where plain code is clearer.`
  - `Chunk size and overlap` — `Tuned against retrieval quality on the target documents.`
  - `FAISS vs ChromaDB` — `Chose the vector store per use case.`
- **Playground** — title `Try it: chunking & retrieval` — caption: `A small in-browser demo. It uses TF-IDF keyword similarity instead of neural embeddings, so you can see how chunk size and overlap change what gets retrieved.`
  - Controls: Chunk size (words) slider 20–120 default 50; Overlap slider 0–40 default 10 (clamped < chunk size); Query input with 3 preset query chips; Top-k fixed 3.
  - Output: `N chunks` count; list of top-3 chunks with rank, score (0–1, 2 decimals), chunk id `#c4`, and query terms highlighted with `<mark>`; a collapsible `Show all chunks` view.
  - Sample corpus (built-in, ~400 words, original text): a short fictional "Engineering handbook" about deployments, versioning, rollback, retries, config, testing. Preset queries: `How does rollback work?`, `What happens to config when an agent version changes?`, `Which tests run before a release?`.
  - Updates live (debounced 150ms). Results region `aria-live="polite"`.

### 8.7 Projects (#projects)
- Eyebrow `Projects` · H2 `Selected work`

**Flagship — Agent Registry** (full-width card)
- Label: `Team project · Covasant` · Title `Agent Registry — AI agent management & deployment platform`
- Summary: `A FastAPI and PostgreSQL control plane to register, configure, version and deploy AI agents across tenants and environments. I built backend features for versioning, promotion, version changes and rollback in a multi-engineer team.`
- `What I built` bullets:
  - `MAJOR.MINOR.PATCH semantic versioning for agent registration and tenant-specific configuration changes.`
  - `Configuration version diffs (e.g. 1.0.0 vs 1.1.0) that flag added, modified and deleted records before promotion, plus environment-specific field highlighting with wildcard JSON paths.`
  - `Tenant-centric promotion: deploy and validate in a lower environment, then promote to higher — with batch-level versioning so the validated version is the promoted version.`
  - `Fleet-wide agent version change: one request moves every tenant on the old version to the new one through a single shared deployment, with per-tenant config overrides and retry-safe reuse.`
  - `Batch rollback settlement that restores state on failure without overwriting changes made since.`
  - `Revision-numbering and record-selection rules extracted into small, pure, unit-tested modules shared across services.`
- Stack tags: Python, FastAPI, Pydantic, SQLAlchemy, PostgreSQL, Alembic, pytest
- **Interactive (2 tabs in the card): `Version diff` | `Promotion`** — caption under both: `Illustrative sample data — not production configuration.`
  - Version diff: sample selector `support-agent 1.0.0 → 1.1.0` and `retrieval-agent 2.1.0 → 2.2.0`; side-by-side on ≥900px, unified on mobile; summary chips `+ added` `~ modified` `− deleted` with counts **computed from the data**. Sample YAML must use neutral keys (no real vendor model names): e.g. `version`, `model: provider-default`, `max_tokens`, `tools`, `retrieval.top_k`, `retrieval.chunk_size`, `retrieval.vector_store: faiss → chromadb`.
  - Promotion stepper: `1 Diff reviewed` → `2 Deploy to lower` → `3 Validate` → `4 Promote to higher`, buttons `Next step` / `Reset`; shows `Batch 1.1.0` badge staying identical through steps; final state text `Same batch version promoted — what was validated is what ships.`
- `<details>` `Read the case study`: Context / Challenge / What I did / Outcome / What I learned — use text from the analysis §10.4, sanitised: no company names besides Covasant, no repo names, no commit ids, no counts. Outcome: `Merged into the shared codebase and covered by unit tests. No production metrics to report publicly.`

**Card — Enterprise RAG system** · tag `GenAI` · `End-to-end RAG pipeline: parsing, chunking, embeddings, FAISS/ChromaDB retrieval and context-aware responses. Compared LangChain and custom implementations; tuned chunk size and retrieval quality.` · link `See the pipeline →` `#rag` · tags LangChain, FAISS, ChromaDB, Python

**Card — Unified ML Framework** · tag `ML platform` · `Configuration-driven framework for supervised and unsupervised models. Preprocessing, model selection, training, evaluation and deployment are automated; new use cases need only datasource and config updates.` · tags Python, FastAPI, scikit-learn, Clean Architecture

**Card — unified-file-reader** · tag `Open source · PyPI` · `Extensible, strongly typed library that reads CSV, JSON, TXT, Excel, PDF, DOCX and more through a single API. Modular design so new formats plug in cleanly.` · links `GitHub` https://github.com/praveen9392/unified-file-reader and `PyPI` https://pypi.org/project/unified-file-reader/ · tags Python, Typing, Packaging

**Small row — Intelligent video-based attendance system** · `Contributed to a video-based attendance system using Python, deep learning and OpenCV.`

### 8.8 How I build (#approach)
- Eyebrow `How I build` · H2 `Spec first, agents second, review always` · lede `I use AI coding agents every day. The spec and the review are what keep the output clean.`
- Flow (5 steps, connected):
  1. `Spec` — `Write the requirement, constraints and acceptance criteria before any code.`
  2. `Plan` — `Agent drafts the plan; I own the module boundaries and data contracts.`
  3. `Build` — `Claude Code, Devin or Google Antigravity implement in small modules; subagents take parallel tasks.`
  4. `Verify` — `Ruff and linting, unit and regression tests, then a human code review.`
  5. `Ship` — `Small, reviewable changes that are easy to roll back.`
- Panel `Tools` — Claude Code · Devin · Google Antigravity
- Panel `How I configure agents` — Custom skills · Subagents · Reusable agent workflows · Global & workspace-specific rules · Context management · Token optimization · Prompt engineering
- Principles row — **Design**: `Clear module boundaries and typed contracts before implementation.` **Build**: `Clean, modular, tested code that a teammate can read in one pass.` **Scale**: `Configuration over code, immutable versions, retry-safe workflows.`

### 8.9 Skills (#skills) — resume only, no percentages, no filters
- Eyebrow `Skills` · H2 `Toolbox`
- Groups (exact):
  - `Languages`: Python, Java, SQL
  - `Backend`: FastAPI, Pydantic, SQLAlchemy, REST APIs, API development, Backend architecture
  - `AI & ML`: Generative AI, RAG, LLM agents, LangChain, Google ADK, NLP, Model training & evaluation
  - `Data`: FAISS, ChromaDB, PostgreSQL, SQLite
  - `AI coding & agentic development`: Claude Code, Devin, Google Antigravity, AI-assisted development, Agentic coding workflows, Spec-driven development
  - `Agent configuration`: Custom skills, Subagents, Reusable agent workflows, Global & workspace rules, Context management, Token optimization, Prompt engineering
  - `Engineering practice`: Git, GitHub, Docker, Ruff, Linting, Clean code, Code reviews, Unit testing, Regression testing, PyPI publishing, Agile, SDLC, STLC
- Layout: 2-column grid of groups (label left, pills right) on desktop; stacked on mobile. Equal visual weight, no orphan card.

### 8.10 Credentials (#credentials)
- Eyebrow `Credentials` · H2 `Education & certifications`
- `B.Tech, Computer Science and Engineering` · `Sreenivasa Institute of Technology and Management Studies` · `2020 – 2024 · CGPA 8.5`
- `Professional Machine Learning Engineer` · `Google`
- `Introduction to Python Programming` · `Microsoft`

### 8.11 Contact (#contact)
- Eyebrow `Contact` · H2 `Let's build something reliable` · lede `Open to backend and GenAI engineering conversations. Email is the fastest way to reach me.`
- Large email row: `bpraveenkumar200321@gmail.com` (mailto) + `Copy` button → toast `Email copied`.
- Secondary: LinkedIn, GitHub. Location line `Based in Hyderabad, India`.
- No form. No phone number.

### 8.12 Footer
`© 2026 Bathala Praveenkumar` · GitHub · LinkedIn · Email · `Back to top`.

## 9. Explicitly removed
AI digital avatar & TTS; "Hire Me"; every resume download/view link and the Resume section; simulated contact form; project modal; skill filter tabs; impact-metric strip with fake numbers; ambient glow blobs; all inline-style one-offs.
