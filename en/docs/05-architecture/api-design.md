---
title: "API Design"
---

# API Design — Parity (`/api/v1`)

> Backend contracts + `architecture-decisions.md` calls.
> Base: Gin (CRUD/auth/matching) + stdlib handler for file transfer only. Auth: Supabase Bearer JWT, role in `app_metadata`.
> **Date:** 2026-09-11.

## Conventions

- JSON; `{code, message}` errors (e.g. `CLIENT_NOT_MAPPED`, `LINE_NEEDS_REVIEW`, `UPLOAD_TOO_LARGE`).
- Listings: `?q=&limit=&offset=` → `{data:[], total}` (proposed convention, for team review during build).
- Line states: `ok | revisar | error | faltante`. `match_por`: `exacto | barra | manual | llm`.
- CORS restricted to the Pages origin.
- Permissions: `empleado` = own/area orders; `admin` = everything + catalog + mappings (Go middleware).

## Endpoints

| Method | Route | What it does | Notes |
|---|---|---|---|
| POST | `/orders/upload` (stdlib, streaming) | Receives Excel (≤10MB) or PDF (cap TBD) via manual upload, stores in Storage, creates `orders` + `order_lines` in `revisar` | Triggers pipeline: Excel→excelize; PDF→pdfcpu+text+LLM. No automatic intake in MVP |
| GET | `/orders/:id` | Order + lines with states and candidates | Includes match origin and candidates per line |
| PATCH | `/orders/:id/lines/:lineId` | Edits line fields (manual or dropdown); changing description→article makes the backend recalculate `codigo` and revalidate state | Dashboard code↔description rule |
| POST | `/orders/:id/lines` | Adds product to the order | Validates against catalog on create |
| DELETE | `/orders/:id/lines/:lineId` | Removes line | Audit log |
| GET | `/orders/:id/export.xlsx` (stdlib) | Generates internal-system Excel format + validation log | Only if no blocking `error`; `revisar` doesn't block but warns |
| GET | `/jobs/:id` | Async job status ("validating with AI…" polling) | pending, processing, done or failed |
| GET | `/catalog?q=&limit=&offset=` | Searches articles (approximate text + trigrams, for the search dropdown) | Candidate ordering: team calibrates |
| GET/POST | `/clients/mappings` | Lists / creates tax-ID→code mapping (admin) | Export prerequisite |
| GET | `/healthz` | Service health | For Render + CI |

## Auth (delegated to Supabase)

Login/refresh/password: `supabase-js` against Supabase Auth directly (the backend does **not** implement login). The backend only validates (Gin middleware → JWKS) and authorizes by role. Self-signup with default `empleado` (admin promotes); Resend emails.
