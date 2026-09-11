---
title: "Decisiones de arquitectura"
description: "ADRs de Parity."
---

# Decisiones de arquitectura

| Decisión | Alternativas | Elección | Motivo |
| --- | --- | --- | --- |
| **Excel parsing** | `tealeg/xlsx`, `excelize` | `excelize` | Soporte .xlsx moderno, límite 10MB, sin CGO. |
| **Base de datos** | MySQL, SQLite | PostgreSQL | Índices para matching y fiabilidad transaccional. |
| **Frontend** | Vue, Angular | React + TypeScript | Ecosistema y tipado para tablas complejas. |
| **Infraestructura** | K8s, VMs | Docker Compose | Suficiente para MVP, sin sobre-ingeniería. |
| **Matching** | Solo código | Código + barra + detección ambigüedad | Cubre duplicados por packaging. |

Cada decisión sigue `Problema → Alternativas → Decisión → Impacto`.
