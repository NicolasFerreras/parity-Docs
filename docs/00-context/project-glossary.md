---
title: "Glosario"
description: "Términos clave de Parity: órdenes, catálogo, matching y validación."
---

# Glosario

| Término | Definición |
| --- | --- |
| **Orden de compra** | Documento del cliente con líneas de productos y cantidades. Puede llegar como Excel, PDF o texto. |
| **Línea de orden** | Fila individual con código, descripción y cantidad solicitada. |
| **Catálogo** | Fuente de verdad de productos: código interno, barras y descripción normalizada. |
| **Código interno** | Identificador único del producto en `articles` (ej. `5271`). |
| **Código de barras** | EAN asociado al producto, usado como clave alternativa para matching. |
| **Matching** | Proceso que clasifica cada línea como exacta, ambigua o fallida al cruzarla con el catálogo. |
| **Validación** | Chequeo de estructura, cantidades y coherencia antes de persistir. |
| **Revisión** | Paso humano donde se corrigen fallidos y se confirma la orden para exportar. |
