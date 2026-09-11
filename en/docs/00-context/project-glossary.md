---
title: "Glossary"
description: "Key terms for Parity: orders, catalog, matching and validation."
---

# Glossary

| Term | Definition |
| --- | --- |
| **Purchase Order** | Client document with product lines and quantities. Can be Excel, PDF or text. |
| **Order Line** | Single row with code, description and requested quantity. |
| **Catalog** | Source of truth for products: internal code, barcodes and normalized description. |
| **Internal Code** | Unique product identifier in `articles` (e.g. `5271`). |
| **Barcode** | EAN associated to the product, used as alternative key for matching. |
| **Matching** | Process that classifies each line as exact, ambiguous or failed when crossing with the catalog. |
| **Validation** | Structure, quantity and coherence checks before persisting. |
| **Review** | Human step where failures are corrected and the order is confirmed for export. |
