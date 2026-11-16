# Functionality & Content Mapping — Old → New

Every element of the old prototype is accounted for: kept, changed, replaced, or removed with a reason.

## Features

| Old feature | Old location | New location / component | Status | Reason |
|---|---|---|---|---|
| Sticky header + anchor nav | Header | Header (Experience · RAG · Projects · How I build · Skills · Contact) | Changed | Reordered around the RAG focus; "Architecture Lab" folded into Projects |
| Mobile drawer | Header | Accessible disclosure menu < 900 px (Esc, focus return) | Improved | A11y |
| Scroll-spy | Global | IntersectionObserver spy, `aria-current`, sliding underline | Improved | Covers every section |
| "Resume ⤓" header button | Header | — | **Removed** | Owner request; file deleted (404) |
| "Hire Me" button | Header | — | **Removed** | Owner request |
| Hero CTAs (View Projects / View Resume / Contact) | Hero | "See the RAG work" / "Get in touch" | Changed | 2 CTAs; resume removed |
| Social links | Hero, Contact, Footer | Hero links row, Contact, Footer | Kept | Email corrected |
| AI Digital Avatar (presets, ask, TTS) | Hero right | Animated RAG pipeline card (hero) + RAG playground (#rag) | **Replaced** | Wrong answers, overclaim, owner dislikes it |
| Highlights strip | After hero | Proof strip (factual labels) | Changed | No fake metrics |
| About + 3 philosophy cards | #about | "What I do" 3 pillars + Design/Build/Scale in #approach | Changed | Owner's themes |
| Experience timeline | #experience | Timeline aligned to the grid, grouped bullets | Changed | Associate Engineer; accurate content |
| Skills filter tabs + 5 cards | #skills | Flat grouped list (7 resume groups) | Changed | Resume-only; no orphan card; no fake tabs |
| 5 project cards | #projects | Flagship (Agent Registry) + 3 cards + 1 small row | Changed | Prioritised |
| Project modal | Overlay | Inline `<details>` case study | Replaced | A11y, mobile |
| Architecture Lab diff (2 samples) | #architecture-lab | Flagship card → "Version diff" tab | Improved | Computed counts, side-by-side, neutral data |
| Simulate Batch Promotion (toasts) | Lab | Flagship card → "Promotion" stepper | Improved | Visible state change |
| Resume hub (download/open, signature) | #resume | — | **Removed** | Owner request; 404; fake data |
| Education + certifications | #resume | #credentials (compact) | Kept | Years removed (not in resume) |
| Contact info cards | #contact | Contact: email row + copy, LinkedIn, GitHub, location | Kept/Changed | Email corrected |
| Contact form (simulated) | #contact | — | **Removed** | Fake success |
| Toasts | Global | Toast for "Email copied" | Kept | — |
| Footer | Footer | Footer + © line | Kept | — |
| — | — | RAG section with pipeline, decisions, playground | **New** | Owner priority |
| — | — | How I build (spec-driven, AI tools, agent config) | **New** | Owner priority |
| — | — | Theme toggle (dark/light) | **New** | Readability |
| — | — | Motion system (intro, canvas, reveals, scroll-linked) | **New** | Owner: "stunning animations" |

## Skills: resume → site (resume is the allow-list)

| Resume group | Site group | Notes |
|---|---|---|
| Programming Languages: Python, Java, SQL | Languages | — |
| Python Backend Development | Backend | — |
| AI & Machine Learning | AI & ML | — |
| Vector Databases + Databases | Data | Merged |
| AI Coding Tools & Agentic Development | AI coding & agentic development | + Spec-driven development (from the resume's agent group) |
| AI Agent Configuration & Workflows | Agent configuration | — |
| Development Tools & Practices | Engineering practice | — |
| scikit-learn, OpenCV, Alembic, pytest | Project tags only | From resume projects / analysis, not in the skills list |

## Content provenance

| Site content | Source |
|---|---|
| Title, company, dates, education, certifications, contact links | Resume p1–2 |
| "Associate Engineer", "started and worked across different parts" | Owner instruction |
| RAG pipeline stages and comparisons | Resume project 4 + skills |
| Agent Registry semver, diff, promotion, batch versioning | Resume project 1 |
| Version change, rollback settlement, revision numbering, env-specific fields, pure modules, stack (Alembic, pytest) | Agent Registry analysis §3, §6, §10 (sanitised) |
| ML framework, unified-file-reader, attendance system | Resume projects 2, 3 + experience |
| AI tools, agent configuration, spec-driven development | Resume skills + owner instruction |
