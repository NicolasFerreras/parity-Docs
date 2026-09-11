# Glosario — Parity

> Vocabulario del dominio (distribuidoras, órdenes de compra, catálogo). Términos universales, sin referencias a casos particulares.

| Término | Definición | Notas |
|---|---|---|
| **Parity** | Producto: estandarizador de órdenes de compra que extrae, mapea y valida datos contra catálogo interno. `parity` (software) / `Parity` (marca) | — |
| **Orden de Compra (OC)** | Documento enviado por el cliente con productos y cantidades. Puede venir como Excel, PDF, texto en mail/WhatsApp o foto. | Pedido |
| **Código interno** | Identificador único del producto en el catálogo (`codigo`, ej. `5271`). Es el que exige el sistema de importación. | SKU interno |
| **Código Proveedor** | Código que usa el proveedor del producto. Aparece en OCs pero no siempre coincide con `codigo`. | — |
| **Código de barras (EAN)** | Hasta 3 EAN por producto (`codbarra`, `codbarra2`, `codbarra3`). Clave para resolver duplicados por cambio de packaging: dos códigos distintos pueden compartir EAN. | EAN-13 |
| **Descripción** | Nombre comercial del producto. Campo ambiguo cuando el cliente escribe genérico. | — |
| **Línea / Proveedor** | Familia/marca del producto. Útil para filtrar búsquedas. | — |
| **Unidades / Display / U. Compra / Cantidad** | Distintas formas de expresar cantidad según cliente (sueltas, packs, bultos/cajas). | Cantidad |
| **Razón social / CUIT / Sucursal** | Identificación del cliente. Las órdenes no siempre traen el código cliente que exige el sistema; solo estos datos. Requiere tabla de mapeo. | — |
| **Matcheo / Matching** | Búsqueda del código interno de cada línea: 1) código exacto, 2) barcode, 3) detección de ambigüedad por descripción. | Estandarización |
| **Ambigüedad** | Descripción que no permite identificar el producto con certeza. Se **detecta y marca** para revisión humana, no se resuelve sola. | — |
| **Duplicados** | Dos códigos distintos con misma descripción visible (cambio de packaging/proveedor). Mayor frustración operativa: retraducción manual. | — |
| **Dashboard tipo Excel** | UI de revisión: grilla editable donde el empleado confirma/corrige antes de exportar. | — |
| **Exportación 1-clic** | Archivo en formato de importación del sistema interno + log de validaciones. | — |

## Abreviaturas comunes

* **CUIT:** Clave Única de Identificación Tributaria (AR)
* **EAN:** European Article Number (barcode)
* **SKU:** Stock Keeping Unit
* **OC:** Orden de Compra
