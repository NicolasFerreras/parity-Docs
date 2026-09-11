---
title: "Reglas de Push — parity-Docs"
description: "Qué se pushea a https://github.com/NicolasFerreras/parity-Docs desde P:\\parity\\docs y qué no, con fuente, MCP y workflow."
---

# Reglas de Push — parity-Docs

> Fuente: `P:\parity\docs` → destino `https://github.com/NicolasFerreras/parity-Docs` (repo separado, `master`/`main`). MCP Mintlify `{"mcpServers":{"Mintlify":{"url":"https://mcp.mintlify.com"}}}` mapeado a `opencode.json:mcp.mintlify` remote. Referencias: `https://www.mintlify.com/docs/components` y `https://www.mintlify.com/docs/organize/settings`.

## Fuente y destino

| Campo | Valor |
|-------|-------|
| **Fuente local** | `P:\parity\docs` (Mintlify `P:\parity\docs.json` en root también se pushea como `docs.json` destino) |
| **Destino** | `https://github.com/NicolasFerreras/parity-Docs` (repo separado `master`/`main`) |
| **MCP** | `Mintlify` `https://mcp.mintlify.com` → `search_mintlify` / `query_docs_filesystem_mintlify` |

## Inclusiones — SIEMPRE pushear

| Carpeta/archivo | Estado actual `P:\parity` | Notas |
|-----------------|---------------------------|-------|
| `00-context/**` | `project-overview.md`, `project-overview.mdx`, `README.md`, `project-glossary.md`, `project-status.md` — completos | Incluido |
| `02-product/**` | `scope.md`, `product-definition.md`, `value-proposition.md`, `business-model-canvas.md`, `mvp-definition.md` — corrige typo `02-pruct` | Incluido (aunque 0B/`TODO`, navegación lo espera) |
| `04-ux/**` | `ux-ui-guidelines.md`, `user-flows.md`, `design-system.md`, `prototype.md` — completos | Incluido |
| `05-architecture/architecture.md` | `TODO` stub | Incluido |
| `05-architecture/architecture-decisions.md` | `TODO` stub | Incluido |
| `05-architecture/api-design.md` | `TODO` stub — corrige `api-desgin` | Incluido |
| `docs.json` | `P:\parity\docs.json` | Incluido (root destino) |
| `favicon.svg`, `logo/**` | `P:\parity\favicon.svg`, `logo/dark.svg` | Incluido si cambia branding |

## Exclusiones — NO pushear

| Carpeta/archivo | Regla | Motivo |
|-----------------|-------|--------|
| `07-domain-data/**` | **NUNCA** | Contiene `product-catalog.md`, `order-format.md` + riesgo `lista_articulos.xlsx` sensible (ya en `.gitignore`) |
| `06-development/**` | **MOMENTÁNEAMENTE** (typo `06-devlopment` corregido) | `coding-conventions`, `git-workflow`, `testing-strategy` aún TODO |
| `05-architecture/class-diagram.md` | NO | Fuera por ahora |
| `05-architecture/data-model.md` | NO | Fuera por ahora |
| `05-architecture/domain-model.md` | NO | Fuera por ahora |
| `05-architecture/er-diagram.md` | NO | Fuera por ahora |
| `03-requirements/**` | NO | `requirements`, `user-stories`, `acceptance-criteria` etc. no pushear |
| `01-research/**` | NO | `research`, `user-persona`, `interviews` etc. no pushear |
| `08-project-management/**` | NO | No pedido |
| `.opencode/**`, `context-map/**`, `Parity Doc/**`, `node_modules/**`, `.git/**` | NUNCA | Solo para agentes locales, Mintlify `docs.json:exclude` |

## Workflow — Documentation Agent

1. Verifica `P:\parity\docs.json` navigation solo lista inclusiones (filtrado `docs.json:41`).
2. Usa Mintlify MCP para componentes (`Card`, `Steps`, `Tip` en `project-overview.mdx`) y `docs.json` settings (`theme: mint`, `colors.primary: #03F07C`, `navigation.groups`).
3. Presenta plan breve (qué/no, archivos, riesgos, reversibilidad) y espera aprobación (`question`).
4. Ejecuta `/publish-docs` → `publish-docs.md` copia filtrada `P:\parity\docs` → repo destino, `mint validate`, `git commit`, `git push` (Human Gate).

Ver `.opencode/commands/publish-docs.md` y `.opencode/agents/documentation.md`.
