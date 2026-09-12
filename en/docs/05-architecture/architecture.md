---
title: "Architecture"
---

# Architecture — Parity

> Based on `architecture-decisions.md` (19 decisions) + `api-design.md`.
> **Date:** 2026-09-11.

## Topology

```mermaid actions={true}
flowchart LR
    subgraph DEV[Local DEV]
        SL[Supabase CLI: PG, Auth, Storage]
        GA[Go API :8080]
        WR[React :5173]
    end
    subgraph PROD[Day-1 cloud PROD]
        SC[Supabase cloud]
        RS[Render web service with keep-alive]
        CF[Cloudflare Pages]
    end
    DEV -.->|CI-CD per repo| PROD
```

Separate repos: Go backend + migrations · React + TypeScript frontend.
CI/CD: GitHub Actions per repo (test + deploy on main).

## PDF flow

```mermaid actions={true}
flowchart TD
    U[Upload PDF] --> S[Storage]
    S --> V[pdfcpu validates]
    V --> T[Text extraction]
    V --> L[LLM answers JSON]
    T --> R[Reconciler: JSON completes or fixes]
    L --> R
    R --> M[Matching against catalog]
    M --> D[Dashboard]
```

## Infrastructure and cross-cutting concerns

- **Type:** modular monolith + layers (decision 12).
- **CORS** restricted to the Pages origin (decision 13).
- **Async jobs:** `jobs` table in PG + Go workers in the same binary (no Redis/Rabbit, decision 14). The dashboard polls job status ("validating with AI…").
- **Retention:** imports deleted on processing; exports 14 days via nightly `pg_cron`; SQL always (decision 15). `/healthz` touches PG to keep the free project alive.
- **Signup:** Supabase self-signup (default `empleado`, admin promotes) + Resend welcome SMTP (decision 16).
- **Errors:** Sentry in Go (decision 17). Grafana → v2.
- **Secrets:** Render env vars (decision 18). No staging: local + prod.

## Data lifecycle

```mermaid actions={true}
flowchart LR
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

## Deferred decisions (don't block initial build)

LLM provider + timeout/fallback, PDF cap, candidate ordering — see decisions and pending spikes.
