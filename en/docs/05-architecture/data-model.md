---
title: "Data Model"
---

# Data Model — Parity (PostgreSQL + Supabase)

> Physical model in PostgreSQL + Supabase.
> Versioned migrations. Required extension: `pg_trgm` (text similarity).
> **Date:** 2026-09-11.

## Indexes (matching)

- `articles(codigo)`, `articles(codbarra, codbarra2, codbarra3)` — exact and barcode search.
- `CREATE INDEX ON articles USING gin (descrip gin_trgm_ops)` — approximate-text + trigram candidates.
- `client_mappings(cuit, razon_social)` — customer resolution.

## Database-level security

- RLS enabled as **second layer**: role policies from the token; the backend operates with the service key and enforces roles in middleware (first layer).
- Files in Supabase Storage: `ordenes/importadas/` (ephemeral, deleted on processing) + `ordenes/exportadas/` (14 days via `pg_cron`); SQL records always. Excel cap 10MB; PDF cap TBD (spike).

## Notes

- `estado DEFAULT 'revisar'`: nothing is `ok` until exact verification.
- `match_por='llm'` implies `estado='revisar'` (application-level rule).
- Candidate ordering and top-N: team calibrates (placeholder, non-blocking).

## Data lifecycle

```mermaid actions={true}
flowchart TD
    U[Upload Excel or PDF] --> S[Imported Storage]
    S --> O[orders and order_lines in review]
    O --> J{jobs}
    J -->|Table PDF| L[LLM and reconciler]
    J -->|Excel or text| M[Matching]
    L --> M
    M --> A[articles and client_mappings]
    M --> G[lines ok, revisar, error, faltante]
    G --> LG[match_logs]
    G --> E[Export xlsx]
    E --> SX[Exported Storage, 14 days]
    S -.->|deleted on processing| X[discarded]
```
