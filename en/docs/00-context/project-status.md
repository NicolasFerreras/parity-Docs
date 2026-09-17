---
title: "Project Status"
---

# Project Status — Parity

> Public document: product status (what exists, what's next), with no case-specific or academic-process information.

## 1. Current Phase

**Documentation complete → Actual phase: Development** The entire definition phase is complete: requirements, architecture, UX/UI, testing, development environment, infrastructure, and deployment. The problem has been validated as real and pressing, the technology stack has been defined, and the remaining 9 stubs are for management/tracking (they do not block coding).

## 2. What Has Been Validated

* **Real-world problem:** Inconsistent formats, different units, duplicates due to packaging changes, and ambiguous descriptions frequently arise in day-to-day operations.
* **Cost:** Tens of minutes per order; ambiguity is the most frequent issue, and duplicates are the most frustrating.
* **Technical feasibility:** A catalog with multiple barcode columns + real orders confirm that exact matching via barcode works; mapping customers by tax ID is feasible.
* **Explicit decision:** Illegible photos are excluded from the MVP (OCR is unreliable; the policy of “requesting a legible resend” remains in place).
* **Technology stack:** Go + React/TypeScript + PostgreSQL. Backend on Render, frontend on Cloudflare Pages, DB + Auth + Storage on Supabase.
* **Requirements:** 10 functional requirements (R-001 to R-010), 5 non-functional requirements (R-NF01 to R-NF05), 10 business rules (RB-001 to RB-010).
* **User Stories:** 9 stories (US1 to US9) with Given/When/Then acceptance criteria and prioritization using the F1-F9 grid.
* **Architecture:** 18 ADRs, modular monolith (Handler → Service → Repository), separate repositories (Go backend / React frontend).
* **Testing:** Documented backend strategy (150–200 tests, 4 quadrants) and frontend strategy (24 tests, FE-01 through FE-24).
* **Development environment:** Local setup with Docker (Supabase CLI), Makefile with standardized commands, documented environment variables.
* **Deployment:** Render (backend) + Cloudflare Pages (frontend) + cron-job.org (keep-alive). CI/CD with GitHub Actions.

## 3. Next Steps

| Area | Status | Next |
|---|---|---|
| Context and Research | ✅ Complete | Keep up to date |
| Product (scope, proposal, MVP) | ✅ Defined | Refine through real-world use |
| Requirements (user stories, criteria, backlog) | ✅ Complete | Traceability: R→US→TC→Impl |
| UX (system, flows, guidelines) | ✅ Defined | Wireframes and user testing |
| Architecture (18 ADRs, diagrams) | ✅ Defined | Spikes: real PDF, LLM, trigrams |
| Testing (backend + frontend) | ✅ Strategy defined | Implement tests according to matrix |
| Environment and deployment | ✅ Configured | Initial local setup + CI/CD |
| Infrastructure and tools | ✅ Documented | — |
| Domain data | ✅ Formats and catalog | Sanitize real catalog for testing |
| Management (roadmap, sprints, risks) | ⏸️ Stubs pending | Complete while developing |
| **Development** | 🔜 **Current phase** | Start US1 (Excel order upload) |

## 4. Active risks and assumptions

* **Input quality:** if the customer sends an illegible photo, the MVP doesn't solve it — "ask for resend" flow.
* **Unconfirmed unit-conversion table:** depends on per-product/customer mapping existing (stretch).
* **LLM pipeline:** per-order cost/latency and commercial-data privacy to evaluate in spike.
* **Free-tier cloud project:** inactivity pauses (mitigated with keep-alive) and bounded file retention.

## 5. Standing decisions

* No OCR in MVP; exact matching before barcode; ambiguity is detected, not guessed.
* Managed authentication (not self-hosted)
* Modular monolith + layers; separate repositories; local dev + staging + prod in the cloud.
* LLM-sourced rows start in `revisar`; `ok` only when identical to catalog.
