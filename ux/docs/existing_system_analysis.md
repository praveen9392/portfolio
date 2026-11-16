# Existing System Analysis — Portfolio Prototype (before redesign)

> Subject: `ux/prototype.html` at commit `0c68c1a` (master). Analysed 2026-11-14.
> Evidence labels: **[Run]** observed in a headless Edge render, **[Code]** read in source, **[Git]** from history.

## A. Product overview

| | |
|---|---|
| What it is | Single-page personal portfolio for Bathala Praveenkumar |
| Problem it solves | Gives recruiters and hiring managers a fast, credible picture of a Python backend / GenAI engineer and a way to make contact |
| Target users | Technical recruiters (fast skim: title, company, dates, stack), engineering managers (depth: architecture, decisions, code quality), peers/clients |
| Primary jobs | 1) Know who he is and what he does in < 10 s; 2) Verify depth on RAG, agents and backend; 3) Contact him |

The research basis for these jobs is in [ux_audit_report.md §1](ux_audit_report.md#1-research-what-works-on-engineer-portfolios).

## B. Technical understanding

| Area | Finding |
|---|---|
| Stack | One static HTML file, 2,968 lines / ~120 KB: ~1,650 lines of inline CSS, ~1,000 lines of markup, ~420 lines of vanilla JS (`PortfolioApplication` class + `PORTFOLIO_CONFIG` object). [Code] |
| Backend / APIs | None. No server, no build step, no package.json, no tests. [Code] |
| External deps | Google Fonts (Plus Jakarta Sans, JetBrains Mono). Web Speech API for avatar TTS. [Code] |
| State | In-memory only (current diff sample). [Code] |
| Assets | `Praveen.pdf` was added in `31222ab` and **deleted in `0c68c1a`**, but four links still point to it. [Git] |
| Docs | `ux/progress.md` records 8 "complete" milestones, including WCAG 2.2 AA and QA claims. Several are contradicted by what was found here (see audit). |

### How it was run
- No build or server is needed. Opened as `file:///C:/workspace2/portfolio/ux/prototype.html`.
- Rendered with headless Microsoft Edge through `playwright-core` at 1440×900, 820×1180 and 390×844, scrolled the full page, and took full-page screenshots.

| Viewport | Page height | Horizontal overflow | Console errors |
|---|---|---|---|
| Desktop 1440 | 8,535 px | 0 px | none |
| Tablet 820 | 10,890 px | **191 px** | none |
| Mobile 390 | 16,127 px | **78 px** | none |

## C. Structure & navigation

```
Header: logo · About · Experience · Skills · Projects · Architecture Lab · Resume · Contact · [Resume ⤓] [Hire Me]
 └ Mobile drawer (same 7 links), toggled by ☰
Main:
 1 Hero (#hero) — intro + 3 CTAs + socials | AI Digital Avatar widget
 2 Highlights strip — 4 "metrics"
 3 About (#about) — 4 paragraphs + 3 philosophy cards
 4 Experience (#experience) — 2-node timeline
 5 Skills (#skills) — 5 filter tabs + 5 category cards
 6 Projects (#projects) — 5 cards + project modal; Architecture Lab (#architecture-lab, a div)
 7 Resume (#resume) — education, certifications, "verified resume" hub
 8 Contact (#contact) — 4 info cards + form
Footer — name, Back to top, LinkedIn, GitHub, Email
Overlays: project modal, toast stack
```

No user roles or auth apply.

## D. Screen / component inventory

| # | Component | Purpose | Actions | Destinations / effect |
|---|---|---|---|---|
| 1 | Header | Brand + nav | 7 anchor links, Resume download, Hire Me, ☰ | Smooth-scroll; download 404s |
| 2 | Hero copy | Identity | View Projects, View Resume (PDF), Contact Me, LinkedIn, GitHub | #projects; PDF 404; #contact; external |
| 3 | AI Digital Avatar | "Grounded agent" Q&A | 4 preset chips, free-text Ask, Voice (TTS) toggle | Keyword lookup → text + speech |
| 4 | Highlights strip | Social proof | — | — |
| 5 | About | Narrative + principles | — | — |
| 6 | Experience timeline | Roles | — | — |
| 7 | Skills | Stack | 5 filter tabs | Show/hide cards |
| 8 | Project cards ×5 | Work samples | View Architecture / Details (modal), GitHub links, Try Live Diff Lab | Modal; external; #architecture-lab |
| 9 | Project modal | Case study | ×, Esc | Close |
| 10 | Architecture Lab | Diff demo | 2 sample tabs, Simulate Batch Promotion | Re-render diff; 2 toasts |
| 11 | Resume hub | Credentials + PDF | Download, Open in Tab | 404 |
| 12 | Contact | Reach out | mailto/LinkedIn/GitHub, form Submit | Simulated "sent" |
| 13 | Footer | Links | 4 links | — |

## E. Functional status

| Feature | Status | Evidence |
|---|---|---|
| Anchor navigation, smooth scroll | Works | [Run] |
| Mobile drawer | Works; no Esc close, no focus management | [Code] |
| Scroll-spy | Partially works. `#architecture-lab` is a `div`, so its nav link never activates | [Code] |
| Skills filter | Works visually; tabs lack `aria-selected` and tabpanels | [Code] |
| Avatar Q&A | **Partially broken.** First-match substring lookup: the "RAG Pipelines" preset returns the *Covasant* answer because "work" matches first. "ML framework" also returns Covasant | [Code + simulated] |
| Avatar TTS | Works where Web Speech exists; it starts speaking on chip click, which can surprise users | [Code] |
| Project modal | Opens/closes; no focus move, focus trap or focus return | [Code] |
| Diff lab | Renders. **Summary counts are hard-coded** (+2 ~1 −1), so they are wrong for the Search Agent sample (+2 ~2 −1). `switchDiffSample` relies on the global `event` | [Code] |
| Simulate Promotion | Two toasts only | [Code] |
| Resume download / view (4 links) | **Broken (404)**: the PDF was removed | [Git] |
| Contact form | **Mocked with a false success.** It validates, waits 1.2 s, says "Message Dispatched Successfully … Praveen has received your inquiry", then discards the message. It also injects the user's name into `innerHTML` | [Code] |

## F. Content accuracy against the resume

| Prototype claim | Resume says | Verdict |
|---|---|---|
| Title "AI Engineer" | "AI Engineer \| Covasant". Owner instruction: present as **Associate Engineer** | Change |
| Email `bpraveenkumark1@gmail.com` | `bpraveenkumar200321@gmail.com` | Mismatch |
| "Led a 4-person engineering team", "cut manual effort by 50%", "30% accuracy" | "Contributed to the development of…" | Invented |
| "sub-50ms query matching", "low latency", "citation transparency" | Not stated | Invented |
| "Multiple Global Clients", "Delivered custom software…for diverse clients" | Not stated | Invented |
| Cert years 2025 / 2022 | No years | Invented |
| "PAGES: 3 (Comprehensive)" | Resume is 2 pages | Wrong |
| Skills: Java & Spring Boot, Hibernate/JDBC, Caching, Task Queues, Monitoring, CI/CD, Face Recognition, Model Fine-Tuning, Sentiment Analysis | Not in resume skills | Remove |
| Missing: AI coding tools (Claude Code, Devin, Antigravity), agent configuration, spec-driven development, Ruff, code reviews, PostgreSQL | In resume | Add |
| Agent Registry role "Lead Backend & Architecture Designer" | Team codebase; specific contributions | Overstated |
| Diff sample uses `gemini-1.5-pro`, `cohere-rerank-v3`, `stripe_invoice_parser` | — | Implies real vendor configs; use neutral sample data |

## G. Known limitations of this analysis
- The page has no backend, so there are no APIs or data models to map.
- Speech synthesis was reviewed in code only. Audio was not tested in headless mode.
- Agent Registry facts come from `C:\workspace\agent-registry\backend\PROJECT_PORTFOLIO_ANALYSIS.md`. That analysis flags that the codebase is proprietary and that authorship is linked by assumption. The redesign uses only sanitised, non-numeric descriptions.
