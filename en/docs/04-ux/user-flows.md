---
title: "User Flows"
description: "How Parity is used end to end."
---

# User Flows

## Main Flow

1. User drags an Excel or PDF to the upload area.
2. Platform extracts lines, validates structure and quantities.
3. System matches each line against the catalog by code or barcode.
4. Table shows results with states and allows editing failures.
5. User confirms and exports in one click.

## Line States

| State | Color | User Action |
| --- | --- | --- |
| **Exact** | Green | None — ready to export. |
| **Ambiguous** | Yellow | Choose among suggested candidates. |
| **Failed** | Red | Correct code or description. |

Goal is 80% of lines in green without intervention.
