---
title: "Architecture"
---

# Arquitectura — Parity

> Basada en `architecture-decisions.md` (ADRs 001–019) + `api-design.md`.
> **Fecha:** 2026-09-11.

## Topología

```mermaid actions={true}
flowchart LR
    subgraph DEV[DEV local]
        SL[Supabase CLI: PG, Auth, Storage]
        GA[API Go :8080]
        WR[React :5173]
    end
    subgraph PROD[PROD nube dia 1]
        SC[Supabase cloud]
        RS[Render web service con keep-alive]
        CF[Cloudflare Pages]
    end
    DEV -.->|CI-CD por repo| PROD
```

Repos separados: backend Go + migraciones · frontend React + TypeScript.
CI/CD: GitHub Actions por repo (test + deploy en main).

## Flujo PDF

```mermaid actions={true}
flowchart TD
    U[Upload PDF] --> S[Storage]
    S --> V[pdfcpu valida]
    V --> T[Extraccion de texto]
    V --> L[LLM responde JSON]
    T --> R[Reconciliador: el JSON completa o corrige]
    L --> R
    R --> M[Matching contra catalogo]
    M --> D[Dashboard]
```

## Infraestructura y transversales

- **Tipo:** monolito modular + capas (ADR-012).
- **CORS** restringido al origen Pages (ADR-013).
- **Trabajos async:** tabla `jobs` en PG + workers Go en el mismo binario (sin Redis/Rabbit, ADR-014). El dashboard consulta estado del job ("validando con IA…").
- **Retención:** import se borra al procesar; export 14 días vía `pg_cron` nocturno; SQL siempre (ADR-015). `/healthz` toca PG para mantener vivo el proyecto free.
- **Registro:** auto-registro Supabase (default `empleado`, admin promueve) + SMTP Resend bienvenida (ADR-016).
- **Errores:** Sentry en Go (ADR-017). Grafana → v2.
- **Secrets:** env vars Render (ADR-018). Sin staging: local + prod.

## Ciclo de vida del dato

```mermaid actions={true}
flowchart LR
    U[Upload Excel o PDF] --> S[Storage importadas]
    S --> O[orders y order_lines en revision]
    O --> J{jobs}
    J -->|PDF-tabla| L[LLM y reconciliador]
    J -->|Excel o texto| M[Matching]
    L --> M
    M --> A[articles y client_mappings]
    M --> G[lineas ok, revisar, error, faltante]
    G --> LG[match_logs]
    G --> E[Export xlsx]
    E --> SX[Storage exportadas, 14 dias]
    S -.->|borrado al procesar| X[descartado]
```

## Decisiones diferidas (no bloquean construcción inicial)

Proveedor LLM + timeout/fallback, tope PDF, ordenamiento candidatos — ver ADRs y spikes pendientes.
