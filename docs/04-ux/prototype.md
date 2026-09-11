---
title: "Prototipo"
description: "Qué permite probar el MVP."
---

# Prototipo

El prototipo valida el flujo sin esperar integraciones externas.

## Qué se puede probar

* Subir un Excel real con 20–100 líneas y ver la clasificación en segundos.
* Buscar en el catálogo por código o barra para resolver ambiguas.
* Editar una línea fallida y ver cómo pasa a exacta.
* Exportar y abrir el archivo resultante en Excel.

## Qué no incluye

* Login o multi-usuario.
* Historial de órdenes o analíticas.
* Integración automática con ERP.

El prototipo está en `src/features/orders` y `src/features/matching` — listo para demos con catálogo del cliente.
