---
title: "Project Glossary"
---

# Glossary — Parity

> Domain vocabulary (distributors, purchase orders, catalog). Universal terms, no case-specific references.

| Term | Definition | Notes |
|---|---|---|
| **Parity** | Product: purchase-order standardizer that extracts, maps and validates data against the internal catalog. `parity` (software) / `Parity` (brand) | — |
| **Purchase Order (PO)** | Document sent by the customer with products and quantities. Can arrive as Excel, PDF, mail/WhatsApp text or photo. | Order |
| **Internal code** | The product's unique identifier in the catalog (`codigo`, e.g. `5271`). Required by the import system. | Internal SKU |
| **Supplier code** | The code used by the product's supplier. Shows up in POs but doesn't always match `codigo`. | — |
| **Barcode (EAN)** | Up to 3 EANs per product (`codbarra`, `codbarra2`, `codbarra3`). Key to resolving packaging-change duplicates: two different codes can share one EAN. | EAN-13 |
| **Description** | The product's commercial name. Ambiguous when the customer writes generically. | — |
| **Line / Supplier** | The product's family/brand. Useful for filtering searches. | — |
| **Units / Display / Purchase unit / Quantity** | Different ways to express quantity per customer (loose units, packs, cases). | Quantity |
| **Business name / Tax ID / Branch** | Customer identification. Orders don't always carry the customer code the system requires; only this data. Needs a mapping table. | — |
| **Matching** | Looking up each line's internal code: 1) exact code, 2) barcode, 3) description-ambiguity detection. | Standardization |
| **Ambiguity** | A description that can't identify the product with certainty. It is **detected and flagged** for human review, never auto-resolved. | — |
| **Duplicates** | Two different codes with the same visible description (packaging/supplier change). Top operational frustration: manual re-translation. | — |
| **Excel-like dashboard** | Review UI: editable grid where the employee confirms/corrects before exporting. | — |
| **1-click export** | File in the internal system's import format + validation log. | — |

## Common abbreviations

* **CUIT:** Argentine tax ID (Clave Única de Identificación Tributaria)
* **EAN:** European Article Number (barcode)
* **SKU:** Stock Keeping Unit
* **PO:** Purchase Order (OC in Spanish)
