# Glosario — Parity

> Fuente léxica: `lista_articulos.xlsx` (catálogo), `OC_N_94325_-_SUCURSAL_ROJAS.xlsx` (orden real), entrevistas y `Clases/UNSAM_PI_Clase 3.md`.

| Término | Definición (en el dominio Raz y Cía) | Sinónimos / Notas |
|---|---|---|
| **Raz y Cía** | Empresa distribuidora de alimentos — caso de estudio. Recibe órdenes de compra de clientes tipo supermercados / almacenes y las factura. | Cliente pagador hipotético de Parity |
| **Parity** | Producto: estandarizador de órdenes de compra que extrae, mapea y valida datos contra catálogo interno. Nombre/branding en `Diseño UX-UI/Logo + nombre final.pdf` | — |
| **Orden de Compra (OC)** | Documento enviado por el cliente con lista de productos y cantidades. Puede venir como Excel, PDF, texto en mail/WhatsApp o foto. Ejemplo real: `OC N 94325 - SUCURSAL ROJAS` (CUIT 30-71674746-4, entrega Rojas 98). | Pedido |
| **Código interno** | Identificador único del producto en el catálogo de Raz y Cía (`codigo` en `lista_articulos.xlsx`, ej. `5271`). Es el que exige el sistema de importación. | SKUs internos |
| **Código Proveedor** | Código que usa el proveedor del producto (ej. `15994` para ALFAJOR BARRIGON). Aparece en OCs pero no siempre coincide con `codigo`. | — |
| **codbarra / codbarra2 / codbarra3** | Hasta 3 códigos de barras EAN por SKU en el catálogo (ej. `7622210964458`, `17622210964479`). Clave para resolver **PP2 duplicados por cambio de packaging**: dos `codigo` distintos pueden compartir el mismo EAN. | EAN-13 |
| **descrip / Descripción** | Nombre comercial del producto (ej. `BUBBALOO 16,5g HUELLITAS FRUT`, `ALFAJOR GUAYMALLEN 38G CHOCOLATE`). Campo ambiguo (PP1) cuando el cliente escribe genérico. | — |
| **linea / Proveedor** | Familia/marca del producto (ej. `ADAMS`, `ARCOR`, `RAZ`). Útil para filtrar búsquedas. | — |
| **Unidades / Display / U. Compra / Cantidad** | Distintas formas de expresar cantidad según cliente (PP6). En `OC_N_94325` se distinguen: `Unidades` (sueltas), `Display` (packs), `U. Compra` (bultos/cajas convertidas). Ej. fila 6: `560 Unidades = 14 Display = 40 U. Compra`. | Cantidad |
| **Costo U. / Total** | Precio unitario y total por línea. Debe validarse contra condiciones comerciales vigentes (promos) — paso del journey “Validación de precios”. | — |
| **Razón social / CUIT / Sucursal / Dirección de entrega** | Identificación del cliente. Crítico porque **PP5**: ninguna de las 3 órdenes reales trae el `código cliente` que exige el sistema; solo traen estos datos. Requiere tabla de mapeo. | — |
| **Matcheo / Matching** | Algoritmo que busca el `codigo` interno correspondiente a una línea de la OC: 1) intento por código exacto, 2) fallback por barcode en las 3 columnas, 3) fallback por descripción (solo detección de ambigüedad en MVP). | Estandarización |
| **Ambigüedad (PP1)** | Cuando la descripción del cliente no permite identificar con certeza el `codigo` (ej. “alfajor guaymallén” sin especificar gramaje/sabor). En MVP se **detecta y marca** para revisión humana, no se resuelve automáticamente. | — |
| **Duplicados (PP2)** | Dos SKUs distintos con misma descripción visible pero `codigo` diferente (por cambio de packaging/proveedor). Mayor frustración reportada por Juan: “retraducción manual”. | — |
| **Unidad/Fracción (PP3)** | Desajuste entre cómo pide el cliente y cómo almacena Raz y Cía (sueltas vs. docena, cajas con distinta cantidad interna). Genera “doble trabajo”: corregir + pedir al cliente orden nueva. | — |
| **Texto libre (PP4a) / Foto borrosa (PP4b)** | Canales no estructurados. PP4a: cuerpo de mail/WhatsApp (“suele pasar seguido” — Juan). PP4b: imagen de baja calidad (“quedan borrosos los números” — fuera de MVP por viabilidad 1/5). | — |
| **Dashboard tipo Excel** | UI propuesta para revisión: grilla editable donde el empleado confirma/corrige el matcheo antes de exportar. Mantiene familiaridad con herramienta actual. | — |
| **Exportación 1-clic** | Generación del archivo en el formato de importación del sistema interno (`Código | Código Proveedor | Descripción | Proveedor | Unidades | Display | U. Compra | Costo U. | Total`). | — |
| **HECHO vs. HIPÓTESIS** | Convención metodológica de Entregable 2 y 3 para distinguir evidencia confirmada por el integrante que trabaja en Raz y Cía (HECHO) vs. supuesto pendiente de validar con encuesta/entrevista (HIPÓTESIS). | Ver `Entregable 2/2.4.Estudio de mercado.docx: User Persona preliminar` |
| **Pain Point / Insight / Oportunidad / Hipótesis** | Vocabulario de Clase 3 (`Clases/UNSAM_PI_Clase 3.md: De los pain points al MVP`). Pain = problema observado, Oportunidad = dirección de mejora, Hipótesis = creencia testeable, MVP = mínimo para probar hipótesis. | — |

## Abreviaturas comunes

* **PP1–PP6:** Pain points numerados en `Analisis/pain_points_a_mvp.md`
* **CUIT:** Clave Única de Identificación Tributaria (AR)
* **EAN:** European Article Number (barcode)
* **SKU:** Stock Keeping Unit
* **OC:** Orden de Compra
