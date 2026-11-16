# Portfolio UX — Progress

## Status
- **Project:** Bathala Praveenkumar — Backend & GenAI engineer portfolio
- **Prototype:** `ux/prototype.html` (single file, no build)
- **Last updated:** 2026-11-14

## 2026-11-14 — Audit & full redesign
The first prototype (2026-11-07) was audited end to end and rebuilt. The earlier "complete" claims in this file (WCAG AA, QA) did not hold up: the audit found broken PDF links, a fake contact-form success, wrong avatar answers, page overflow on tablet and mobile, and invented resume claims.

| Deliverable | File |
|---|---|
| Existing system analysis | [docs/existing_system_analysis.md](docs/existing_system_analysis.md) |
| Screen-by-screen audit | [docs/screen_audit.md](docs/screen_audit.md) |
| UX audit, research & keep/cut/add | [docs/ux_audit_report.md](docs/ux_audit_report.md) |
| Redesign strategy & exact content spec | [docs/redesign_strategy.md](docs/redesign_strategy.md) |
| Old → new mapping & content provenance | [docs/functionality_mapping.md](docs/functionality_mapping.md) |
| Validation | [docs/validation_report.md](docs/validation_report.md) |

### Key decisions
- Positioned as **Associate Engineer at Covasant**, with RAG and backend leading and AI-assisted (spec-driven) engineering as the differentiator.
- Removed: AI avatar, Hire Me, all resume download/view, simulated form, fake metrics, non-resume skills.
- Added: RAG section with a working chunking & retrieval playground; Agent Registry flagship with diff and promotion demos; How I build; Design/Build/Scale; light/dark theme; full motion system (reduced-motion safe).

## 2026-11-15 — v2 clarity pass
Applied [docs/portfolio_clarity_review.md](docs/portfolio_clarity_review.md) through [docs/clarity_changes_spec.md](docs/clarity_changes_spec.md):
- Plain-language hero with quick facts and a "What I can help with" card. One "Email me" button.
- Nav: About · Experience · Projects · Open source · Skills · Contact.
- One project card format (problem / my role / result). The RAG deep dive and demos sit behind "Technical details".
- New Open source section. Skills split into Strong / Working knowledge.
- Middle-path motion: the canvas, typing, tilt, magnetic buttons and count-ups are removed.

Owner decisions: no open-to status; no cert years, links or reply time.

## 2026-11-15 — v3 (review v2)
Applied [docs/review_v2_changes_spec.md](docs/review_v2_changes_spec.md): colour-as-wayfinding, larger type, alternating sections, plain headline with a gradient keyword, computed years, the "Ask → Find → Answer" hero card, service tiles, stats band, About story, demo thumbnails, impact-first results, architecture diagram, PyPI badges, grouped skills, favicon, print stylesheet.

### Open items
- Needs owner input: photo + og:image, availability badge, cert years/links, reply time, booking link, testimonials, real impact numbers.
- Cross-browser (Firefox/Safari) and screen-reader testing.
- Owner to confirm the employer policy on Agent Registry details before publishing.
- Production build/hosting not started (the prototype is a static file).
