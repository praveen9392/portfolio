# UX Audit Report — What to Keep, What to Cut, What to Add

> Audience: the portfolio owner, and anyone reviewing the redesign.
> Inputs: the current prototype ([existing_system_analysis.md](existing_system_analysis.md), [screen_audit.md](screen_audit.md)), the resume `Praveen (1).pdf`, the sanitised Agent Registry analysis, and web research (sources in §6).

---

## 1. Research: what works on engineer portfolios

| # | Finding | Implication for this site |
|---|---|---|
| R1 | In TheLadders' eye-tracking study (30 recruiters), the first pass took about **6–7 s**, and roughly 80% of it went to **name, titles, companies, dates and education**. This is resume data, but the first-skim behaviour carries over. | Name, **Associate Engineer · Covasant**, and the focus area (backend + RAG) must be readable above the fold without scrolling or interaction. |
| R2 | Hiring-manager write-ups agree that **skill percentage bars** are criticised almost universally; list technologies with context instead. | Plain grouped pills, no proficiency scores. The old site already avoided bars; keep it that way. |
| R3 | **2–5 strong projects** beat many; too many projects bury the best work. | One flagship (Agent Registry) and one featured topic (RAG), then 3 compact supporting cards. |
| R4 | Broken mobile layouts and **broken links** are named credibility hits. | Fix overflow and remove the dead PDF links. |
| R5 | Strong AI/RAG portfolio pieces show **the user problem, the pipeline, the decisions, evaluation and citations**, not a generic chatbot demo. | Replace the avatar with a pipeline explainer, a "what I compared" panel and a working retrieval playground. |
| R6 | Reviewers judge **code quality, modular architecture, tests and docs**; the site is the entry point, not the proof. | Put clean, modular, tested code front and centre in copy, link GitHub and PyPI, and describe architecture decisions. |
| R7 | Slow or flashy sites cost time for reviewers who spend about 3 minutes (vendor estimate, unverified). | Rich motion is fine only if it never blocks reading: GPU-only animation, a short intro, and reduced-motion respected. |
| R8 | No research found on how hiring managers view portfolio chatbots. Several engineers do build CV-grounded RAG bots, but as real retrieval systems with sources. | A keyword matcher that claims to be a "grounded agent" is the risky version of a reasonable idea. |

## 2. Keep / Cut / Add

### Keep (good in the current prototype)
- Dark, technical aesthetic and the mono + sans pairing (refined, not replaced).
- Anchor-based single page with a sticky header and scroll-spy.
- The **version-diff lab**, the best proof element (fixed and promoted into the flagship card).
- Grouped skills without percentages.
- Semantic landmarks, skip link, focus rings and the reduced-motion query, as a starting point.
- Education and certifications, made compact.

### Cut
| Item | Reason |
|---|---|
| AI Digital Avatar + TTS | Owner dislikes it. It gives wrong answers, contains invented facts, and overstates a keyword lookup as an agent (R5, R8). |
| "Hire Me" button | Owner request. One of 5 competing CTAs. |
| All resume download/view links and the Resume hub | Owner request. All 4 links are 404s. Fake "document signature". |
| Simulated contact form | False success state; messages are lost. |
| Metrics strip ("100%", "v1.0.0+") | Labels posing as metrics. |
| Invented claims (team lead, 50%, 30%, sub-50ms, global clients, cert years, "3 pages") | Not in the resume; risky in interviews. |
| Non-resume skills (Java Spring Boot, Hibernate, caching, task queues, CI/CD, monitoring, face recognition, fine-tuning, sentiment analysis) | Owner request: resume skills only. |
| Project modal, skill filter tabs | Accessibility debt for little value; replaced by inline disclosure and a flat grouped list. |

### Add
| Item | Why |
|---|---|
| **Associate Engineer** title + "started here, worked across different parts of the stack" story | Owner request; accurate and it explains the breadth. |
| **RAG section** (6-stage pipeline, decisions, live chunking & retrieval playground) | Owner's top priority; R5. |
| **Agent Registry flagship** with sanitised contributions: semver, diffs, promotion, fleet-wide version change, rollback settlement, pure tested modules | Strongest backend evidence (from the analysis); R3, R6. |
| **How I build**: spec-driven development with Claude Code, Devin, Google Antigravity; custom skills, subagents, rules, context & token management | Owner request; a 2026 differentiator. |
| **Design → Build → Scale** principles | Owner: "I can design, build, scale efficiently". |
| Missing resume skills (AI coding & agent configuration groups, Ruff, code reviews, PostgreSQL) | Resume completeness. |
| Correct email, PyPI link | Accuracy. |
| Cinematic motion system (see [redesign_strategy.md §5](redesign_strategy.md#5-motion--every-section-should-be-felt-owner-requirement-2026-11-14)) | Owner: visitors should feel every section. |
| Light theme | Readability preference, plus print and projector use. |

## 3. Prioritised findings

| ID | Area | Problem | User impact | Sev | Fix in redesign |
|---|---|---|---|---|---|
| F1 | Contact | Form fakes "sent" and discards the message | Lost opportunities; the visitor feels misled | Critical | Direct email + copy button, LinkedIn, GitHub |
| F2 | Resume links | 4 links to a deleted PDF | Dead ends; feels unfinished | Critical | Removed (owner request) |
| F3 | Responsive | 191 px (tablet) / 78 px (mobile) page overflow, a crowded header, and project cards wider than the viewport | Sideways scrolling, clipped UI on phones, where many recruiters first open links | Critical | Mobile-first grid, `minmax(min(100%, …))`, a menu below 900 px |
| F4 | Avatar | Wrong answers (RAG chip → Covasant), invented facts, "agent" overclaim | Undermines GenAI credibility | Critical | Removed; replaced by an honest, working RAG playground |
| F5 | Content | Invented metrics and claims; email mismatch; wrong title | Interview risk; trust | High | All copy traced to the resume and analysis |
| F6 | Positioning | RAG/backend not leading; no AI-tooling story | Misses the owner's differentiators | High | Hero + RAG section + How I build |
| F7 | Alignment | Timeline offset from the section grid; orphan skill card; 3+2 project grid; ragged card footers; uneven About columns | Feels unpolished ("sections not properly aligned") | High | One container, one left edge, grids sized to item counts, footers pinned |
| F8 | CTAs | 5 competing actions above the fold | Diluted intent | High | 2 CTAs: "See the RAG work", "Get in touch" |
| F9 | Diff lab | Hard-coded, wrong counts; promotion is toasts only | A careful reviewer spots the bug | High | Counts computed from data; a visual stepper |
| F10 | A11y | Muted text ~3.9:1; modal without focus management; tabs without ARIA; TTS on by default | Excludes some users; fails WCAG 2.2 AA | Medium | Tokens ≥4.5:1, no modal, full tab pattern, no autoplay audio |
| F11 | Hero layout | 100vh centring creates dead space; the role line wraps badly on mobile | Weaker first impression | Medium | Content-sized hero, balanced 2-column |
| F12 | Code hygiene | 60+ inline styles, innerHTML with user input, global `event` | Maintenance; self-XSS | Medium | Classes and tokens only; escaped rendering |
| F13 | Motion | Mostly static | Doesn't meet the "stunning" goal | Medium | Full motion system, reduced-motion safe |

## 4. Content positioning (summary)

- **Headline:** "I design, build and scale backend systems for GenAI."
- **Who:** Associate Engineer at Covasant. Python/FastAPI. Started there and worked across retrieval, agent platforms, an ML framework and APIs.
- **Proof order:** RAG pipeline → Agent Registry backend → How I build with AI agents → supporting projects → skills → credentials.
- **Tone:** specific, verifiable, no superlatives, no numbers that aren't in the resume.

## 5. Confidentiality note for the owner
The Agent Registry source is a proprietary client codebase. The redesign names no client, repository, host, ticket or commit, quotes no codebase statistics, and labels all demo data as illustrative. **Check Covasant's (and its client's) policy before publishing.** If in doubt, replace the flagship's "What I built" bullets with the four resume bullets only.

## 6. Sources
- [TheLadders eye-tracking coverage — Business Insider](https://www.businessinsider.in/what-recruiters-look-at-in-the-6-seconds-they-spend-on-your-resume/articleshow/45040460.cms)
- [What recruiters look for on your CV — World Economic Forum](https://weforum.org/stories/2014/11/what-recruiters-look-your-cv-resume)
- [How long recruiters spend on a resume — Hiration](https://www.hiration.com/blog/how-long-recruiters-spend-on-resume/)
- [What 60+ hiring managers look for in developer portfolios](https://soychristian.pages.dev/contents/developer-portfolio-guide)
- [Common web developer portfolio mistakes — Scrimba](https://scrimba.com/articles/web-developer-portfolio-mistakes/)
- [How to build a web developer portfolio that gets you hired — Scrimba](https://scrimba.com/articles/how-to-build-a-web-developer-portfolio-that-gets-you-hired)
- [Developer portfolio checklist — DevPlaybook](https://devplaybook.cc/blog/developer-portfolio-checklist-20-things-hiring-managers)
- [Hiring managers don't care about your portfolio website — DEV](https://dev.to/oseni03/hiring-managers-dont-care-about-your-portfolio-website-heres-what-they-do-care-about-30lf)
- [Portfolio content for tech jobs — scale.jobs](https://scale.jobs/blog/portfolio-content-for-tech-jobs-what-recruiters-want)
- [AI engineering portfolio projects — DataTalks.Club](https://datatalks.club/podwiki/wiki/ai-engineering-portfolio-projects/)
- [RAG portfolio projects — DataTalks.Club](https://datatalks.club/podwiki/wiki/rag-portfolio-projects/)
- [RAG-on-me (CV-grounded RAG example)](https://solvin-it.github.io/projects/rag-on-me/)

Most sources are career blogs; the only primary study is TheLadders (small sample, resume-focused). Treat the research as directional.
