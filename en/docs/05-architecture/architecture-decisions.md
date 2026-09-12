---
title: "Architecture Decisions"
---

# Architecture Decisions — Parity

> Standing decision list. Each follows Problem → Alternatives → Decision → Consequences. Traceable to team decisions on record.
> **Date:** 2026-09-11.

- **HTTP framework (Gin + stdlib):** Gin for CRUD, auth and matching; stdlib only for file upload/download streaming. Mandatory rule: no business logic in the file handler.
- **Migrations (Goose):** versioned SQL schema; CI applies `goose up` in prod.
- **Managed auth (Supabase Auth):** reasoned reversal of homegrown JWT (homegrown auth concentrates risk). Login with client library, backend validates signature and authorizes by role (`admin` | `empleado`); RLS as second layer. First admin seeded by hand.
- **Environments (local dev, day-1 cloud prod):** 100% local development with Docker stack; only verified code reaches cloud.
- **Cloud (Supabase + Render):** Supabase as Postgres + Storage + Auth; Render as API + frontend. Only those uses without a new decision. Free project with keep-alive.
- **Separate repos:** Go backend + migrations on one side, React frontend on the other, with frozen API contracts.
- **Excel (excelize) and PDF in parallel:** Excel with standard library; PDF with validator + text extractor, with mandatory prior spike against a real PDF. Gotenberg discarded (it's conversion, not extraction); `unipdf` discarded over commercial licensing.
- **Deterministic ambiguity:** candidates by approximate text + trigrams (`pg_trgm`); the employee picks, the system never picks alone.
- **LLM only for table PDFs:** runs alongside the library before matching; the JSON completes or fixes extraction. Every LLM-sourced row starts in `revisar`. Provider, timeouts and privacy to define in spike. No LLM for Excel.
- **4 states, binary ok:** `ok` only when identical to catalog; any touch-up → `revisar`; invalid data → `error`; missing data → `faltante`.
- **No OCR in MVP:** illegible photos out; graceful "ask for legible resend" exit.
- **Type (modular monolith + layers):** Handler → Service → Repository in one Go binary + SPA. Microservices only by future decision.
- **Restricted CORS:** frontend origin only, configured per environment.
- **Async in PG + Go workers (no Redis/Rabbit):** the bottleneck is the LLM (seconds), not Go; at this scale (2–5 concurrent) an in-process pool + PG states gives durability and visibility with no network hop, failure point or extra secret.
- **Retention:** ephemeral imports (deleted on processing), 14-day exports via nightly `pg_cron`, SQL always (auditing intact).
- **Signup and SMTP:** Supabase self-signup (default `empleado`, admin promotes); Resend for welcome emails.
- **Errors and observability:** Sentry from day 1; in-house metric dashboards deferred to v2.
- **Tier and secrets:** free tier with keep-alive ping; secrets as service env vars; no staging (local + prod); default domains (`*.pages.dev`, `*.onrender.com`).
- **No bot, no automatic intake:** conversational bot discarded; MVP is manual upload only. Future automatic intake needs its own decision.
