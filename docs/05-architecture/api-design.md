---
title: "Diseño de API"
description: "Contratos HTTP de Parity."
---

# Diseño de API

## Principios

* REST JSON, prefijo `/api/v1`.
* Códigos HTTP correctos (400 validación, 422 no procesable, 500 error interno).
* Respuestas uniformes `{ code, message, details }`.

## Recursos principales

| Recurso | Método | Descripción |
| --- | --- | --- |
| `POST /orders/import` | Importa Excel/PDF y devuelve `orderId` + líneas validadas. |
| `GET /orders/{id}` | Consulta orden con estados `exact / ambiguous / failed`. |
| `POST /orders/{id}/export` | Exporta al formato interno tras revisión. |
| `GET /catalog?query=` | Búsqueda por código o barra para revisión manual. |

## Autenticación

Fuera de MVP. Cuando aplique, se usará token por cabecera `Authorization`.

Toda validación se hace en servidor; el frontend valida espejo pero no sustituye.
