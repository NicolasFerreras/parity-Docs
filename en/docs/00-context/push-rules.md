---
title: "Push Rules — parity-Docs"
description: "What is pushed to https://github.com/NicolasFerreras/parity-Docs from P:\\parity\\docs and what is not."
---

# Push Rules — parity-Docs

> Source: `P:\parity\docs` → Destination `https://github.com/NicolasFerreras/parity-Docs` (separate repo, `master`/`main`). Mintlify MCP `https://mcp.mintlify.com`.

## Source and Destination

| Field | Value |
|-------|-------|
| **Local source** | `P:\parity\docs` (Mintlify `docs.json` at root also pushed) |
| **Destination** | `https://github.com/NicolasFerreras/parity-Docs` |
| **MCP** | `Mintlify` `https://mcp.mintlify.com` |

## Always Include

| Folder/file | Notes |
|-------------|-------|
| `00-context/**` | project-overview, glossary, status — complete |
| `02-product/**` | scope, product-definition, value-proposition, BMC, mvp-definition |
| `04-ux/**` | ux-ui-guidelines, user-flows, design-system, prototype |
| `05-architecture/architecture.md` | TODO stub |
| `05-architecture/architecture-decisions.md` | TODO stub |
| `05-architecture/api-design.md` | TODO stub |
| `docs.json`, `favicon.svg`, `logo/**` | Branding |

## Never Include

| Folder/file | Rule | Reason |
|-------------|------|--------|
| `07-domain-data/**` | **NEVER** | Contains sensitive `lista_articulos.xlsx` |
| `06-development/**` | **MOMENTARILY** | Still TODO |
| `05-architecture/{class-diagram,data-model,domain-model,er-diagram}.md` | NO | Out of scope for now |
| `03-requirements/**` | NO | Internal |
| `01-research/**` | NO | Internal |
| `08-project-management/**` | NO | Not requested |
| `.opencode/**`, `context-map/**` | NEVER | Agents only |

## Workflow — Documentation Agent

1. Verify `docs.json` navigation only lists inclusions.
2. Use Mintlify MCP for components and settings.
3. Present brief plan (what/not, files, risks, reversibility) and wait for approval (`question`).
4. Execute `/publish-docs` → filtered copy → `mint validate` → `git commit` → `git push` (Human Gate).

See `.opencode/commands/publish-docs.md`.
