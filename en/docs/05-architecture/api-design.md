---
title: "API Design"
description: "Parity HTTP contracts."
---

# API Design

## Principles

* REST JSON, prefix `/api/v1`.
* Correct HTTP codes (400 validation, 422 unprocessable, 500 internal error).
* Uniform responses `{ code, message, details }`.

## Main Resources

| Resource | Method | Description |
| --- | --- | --- |
| `POST /orders/import` | Imports Excel/PDF and returns `orderId` + validated lines. |
| `GET /orders/{id}` | Fetches order with states `exact / ambiguous / failed`. |
| `POST /orders/{id}/export` | Exports to internal format after review. |
| `GET /catalog?query=` | Search by code or barcode for manual review. |

## Authentication

Out of MVP. When applicable, token via `Authorization` header.

All validation happens on server; frontend mirrors but does not replace.
