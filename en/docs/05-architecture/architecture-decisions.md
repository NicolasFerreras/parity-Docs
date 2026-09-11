---
title: "Architecture Decisions"
description: "Parity ADRs."
---

# Architecture Decisions

| Decision | Alternatives | Choice | Reason |
| --- | --- | --- | --- |
| **Excel parsing** | `tealeg/xlsx`, `excelize` | `excelize` | Modern .xlsx support, 10MB limit, no CGO. |
| **Database** | MySQL, SQLite | PostgreSQL | Indexes for matching and transactional reliability. |
| **Frontend** | Vue, Angular | React + TypeScript | Ecosystem and typing for complex tables. |
| **Infrastructure** | K8s, VMs | Docker Compose | Enough for MVP, no over-engineering. |
| **Matching** | Code only | Code + barcode + ambiguity detection | Covers packaging duplicates. |

Each decision follows `Problem → Alternatives → Decision → Impact`.
