---
title: "Glossary — Parity"
description: "Domain glossary for distributors, orders, catalog and matching."
---

# Glossary — Parity

| Term | Definition | Notes |
|------|------------|-------|
| **Generic Distributor** | Food distribution company — initial anonymized case, scalable to multiple distributors. Receives purchase orders from supermarkets/warehouses. | Payer hypothesis for Parity |
| **Purchase Order (PO)** | Document sent by the client with product list and quantities. Can be Excel, PDF, mail/WhatsApp text or photo. Example: `OC N 94325` | Order |
| **Internal Code** | Unique product identifier in the distributor's catalog (`codigo` in `lista_articulos.xlsx`, e.g. `5271`). Required by import system. | SKUs |
| **Barcode** | Up to 3 EANs per SKU (`codbarra`, `codbarra2`, `codbarra3`). Key for PP2 duplicates after packaging change. | EAN-13 |
| **Description** | Commercial name (e.g. `BUBBALOO 16,5g`). Ambiguous field (PP1) when client writes generic text. | — |
| **Matching** | Algorithm that finds the internal `codigo` for a PO line: 1) exact code, 2) barcode fallback, 3) description (MVP only detects ambiguity). | Standardization |
