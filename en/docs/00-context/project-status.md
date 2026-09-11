---
title: "Project Status"
description: "What exists today, what is in progress and next priorities for Parity."
---

# Project Status

Parity is in an MVP foundation phase. The platform already has the base architecture, infrastructure and several business modules, but the full end-to-end flow is still being hardened.

## Current Stage

The project is past the prototype stage. It already has separate repositories, database persistence, documentation and API specs.

The main goal now is to connect the product loops end to end:

<CardGroup cols={2}>
  <Card title="Import loop" icon="file-spreadsheet">
    User uploads Excel or PDF, platform extracts and validates lines and generates a preview.
  </Card>
  <Card title="Matching loop" icon="git-compare">
    Platform matches each line against the catalog by code or barcode and marks exact, ambiguous and failed.
  </Card>
  <Card title="Review loop" icon="table">
    User reviews in a table, corrects failures and exports in one click to the internal format.
  </Card>
  <Card title="Observability loop" icon="activity">
    Structured logs and validation allow auditing what was imported and how it was resolved.
  </Card>
</CardGroup>

## What Exists Today

| Area | Status | Operational Meaning |
| --- | --- | --- |
| Documentation | Active on Mintlify | Product, technical and operations centralized. |
| API | Go + PostgreSQL on Docker | Orchestrates validation, matching and persistence. |
| Interface | React + TypeScript | Upload, review and manual editing. |
| Catalog | PostgreSQL | Durable source of products and codes. |
| Infrastructure | Docker Compose | Reproducible stack locally and in production. |

## Next Priorities

1. Validate end-to-end Excel import and code/barcode matching.
2. Harden the API contract before the frontend depends heavily on it.
3. Complete frontend/API integration with consistent loading and error states.
4. Sync the OpenAPI spec in the docs repository.
5. Define the bilingual documentation workflow before translating every page.
