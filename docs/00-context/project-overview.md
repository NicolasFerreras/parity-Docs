---
title: "Project Overview"
---

# Project Overview — Parity

> Documento público. Tono B2B universal: describe el producto para cualquier distribuidora, sin datos de casos particulares.

## 1. Elevator pitch

**Parity — Estandarización de Órdenes de Compra**. Parity recibe la orden de compra tal como la envía el cliente (WhatsApp, email, PDF, Excel, foto), la interpreta automáticamente contra el catálogo interno y la deja lista en un dashboard tipo Excel para revisión humana en **segundos**, no en decenas de minutos. No reemplaza al empleado: **lo asiste** — cuando algo es ambiguo, lo señala para que decida.

## 2. Problema

En una distribuidora la recepción y carga de órdenes exige un formato determinado (`código producto + descripción + cantidad`), pero:

* Las órdenes llegan por **múltiples canales** sin formato único (WhatsApp, correo, PDF, Excel, fotos).
* Cada cliente usa **sus propios códigos, su propia forma de describir productos y su propia lógica de cantidades** (cajas, unidades, display, bulto).
* Hoy un empleado traduce todo **a mano**: busca a qué producto corresponde cada código, corrige unidades, resuelve ambigüedades a criterio propio.

**Impacto típico:** hasta 30 minutos por orden y una porción significativa de la jornada operativa dedicada a validación; la mayoría de los usuarios relevados cree que el proceso podría ser más simple y rápido.

## 3. Para quién

* **Usuarios directos:** empleados administrativos, de facturación, logística y ventas que reciben, verifican y cargan órdenes.
* **Comprador:** la distribuidora como organización (licencia).
* **Usuarios indirectos:** los clientes que generan las órdenes (no usan Parity, pero determinan los formatos).

## 4. Solución propuesta (flujo TO-BE)

```
Orden llega (cualquier canal) → Extracción + Matcheo contra catálogo → Dashboard tipo Excel para revisión → Empleado confirma/corrige → Exportación 1-clic al formato del sistema interno
```

* **Matcheo:** código exacto + código de barras (hasta 3 EAN por producto). Tabla de mapeo `razón social / CUIT / sucursal → código cliente interno`.
* **Detección de ambigüedad:** marca, no resuelve automáticamente (principio "no reemplazar criterio humano").
* **Exportación:** formato de importación del sistema interno + log de validaciones para auditoría.

## 5. Componentes principales del sistema

| Componente | Propósito |
|---|---|
| App web | Registro, login, subida de órdenes y dashboard de revisión. |
| API | Backend de negocio y fuente de verdad (órdenes, catálogo, validaciones). |
| PostgreSQL | Fuente durable de verdad. |
| Storage | Archivos importados (efímeros) y exportados (retención 14 días). |
| Auth gestionado | Registro, login y tokens JWT. |
| Pipeline PDF + LLM | Extrae y estructura pedidos en PDF antes del matching. |
| Sentry | Errores y caídas en producción. |

## 6. Alcance MVP vs. visión

| Dentro del MVP | Stretch (si alcanza el tiempo) | Explícitamente fuera |
|---|---|---|
| Detección de código de cliente (prerrequisito: sin esto no se exporta) | Texto libre (requiere pipeline LLM propio) | OCR sobre fotos ilegibles (salida digna: pedir reenvío legible) |
| Matching por código exacto + barras | Cantidades por cliente, conversión de unidades | |
| Importación/exportación de documentos | Visualización de catálogo | |
| Detección (no resolución) de ambigüedad | | |

## 7. Métricas de éxito

* Tiempo por orden: decenas de minutos → menos de 5 (meta 2).
* % de líneas matcheadas automáticamente sin intervención.
* % de ambigüedades detectadas vs. no detectadas (falsos negativos).
* Reducción de errores de facturación por código/cantidad equivocada.

## 8. Etapa actual

Fase fundacional de MVP: monolito modular + SPA con servicios gestionados. Objetivo: validar el ciclo central (orden entra → pedido validado sale) antes de infraestructura más pesada. Detalle en `project-status.md`.
