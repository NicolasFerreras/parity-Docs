---
title: "Project Status"
---

# Project Status — Parity

> Public document: product status (what exists, what's next), with no case-specific or academic-process information.

## 1. Current phase

Discovery done → product and architecture definition. The problem is validated as real and painful (lost operating time, 4 recurring symptoms, medium-high frustration, widely recognized room for improvement) and the proposed matching as viable with real data.

## 2. What's validated

* **Real problem:** heterogeneous formats, mismatched units, packaging-change duplicates and ambiguous descriptions show up frequently in daily operations.
* **Cost:** tens of minutes per order; ambiguity is the most frequent symptom, duplicates the most frustrating.
* **Technical viability:** a catalog with multiple barcode columns + real orders confirm exact+barcode matching works; customer mapping from fiscal data is feasible.
* **Explicit decision:** illegible photos out of the MVP (unreliable OCR; keep "ask for legible resend").

## 3. Next steps

| Area | Status | Next |
|---|---|---|
| Context & research | Complete | Keep updated |
| Product (scope, proposition, MVP) | Defined | Refine with real usage |
| Requirements (prioritization) | Grid complete | Stories, criteria and backlog |
| UX (system, flows, prototype) | Defined | Wireframes and user tests |
| Architecture | Defined (19 ADRs) | Spikes: real PDF, LLM, trigrams |
| Development | Pending | Conventions, testing, CI/CD |
| Domain data | Pending | Formats and sanitized catalog |
| Management | Pending | Roadmap, sprints, risks |

## 4. Active risks and assumptions

* **Input quality:** if the customer sends an illegible photo, the MVP doesn't solve it — "ask for resend" flow.
* **Unconfirmed unit-conversion table:** depends on per-product/customer mapping existing (stretch).
* **LLM pipeline:** per-order cost/latency and commercial-data privacy to evaluate in spike.
* **Free-tier cloud project:** inactivity pauses (mitigated with keep-alive) and bounded file retention.

## 5. Standing decisions

* No OCR in MVP; exact matching before barcode; ambiguity is detected, not guessed.
* Managed auth (not homegrown); modular monolith + layers; separate repos; local dev + cloud prod.
* LLM-sourced rows start in `revisar`; `ok` only when identical to catalog.
