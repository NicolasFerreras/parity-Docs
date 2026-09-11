# Project Overview — Parity

> **Proyecto Integrador I — UNSAM / Escuela de Ciencia y Tecnología — 2026**
> Equipo: Parolari Demian (44451375) · Macri Dante (46266095) · Franceschelli Lucas (44160996) · Rusconi Rocío (37140272) · Ferreras Nicolás Agustín (46556419) · Docentes: Esp. Ing. Andrea Alegretti · Ing. Silvina Novoa

## 1. Elevator pitch

**Parity — Estandarización de Órdenes de Compra**. Parity recibe la orden de compra tal como la envía el cliente (WhatsApp, email, PDF, Excel, foto) , la interpreta automáticamente contra el catálogo interno de **Raz y Cía** (distribuidora de alimentos, caso de estudio) y la deja lista en un dashboard tipo Excel para revisión humana en **segundos**, no en 20–30 minutos. No reemplaza al empleado: **lo asiste** — cuando algo es ambiguo, lo señala para que decida.

Fuente: `Entregables facu/Documentacion de proyecto/Resumen.txt:1-13` y `Relevamiento y Descubrimiento/1.2.Template Formulación inicial_V1.2.docx:41-62`.

## 2. Problema

En Raz y Cía la recepción y carga de órdenes requiere que la información cumpla un formato determinado (`código producto + descripción + cantidad`), pero:

* Las órdenes llegan por **5+ canales** sin formato único (WhatsApp, correo, PDF, Excel, imágenes/fotos de baja calidad). Fuente: `Relevamiento/1.2.Template:28` + `Entrevista Transcripción 00:01:23`.
* Cada cliente usa **sus propios códigos, su propia forma de describir productos y su propia lógica de cantidades** (cajas, unidades, display, bulto).
* Hoy un empleado traduce todo **a mano**: busca a qué producto corresponde cada código, corrige unidades, resuelve ambigüedades por criterio propio o consultando a un compañero.

**Impacto medido:**

* Entrevista a Juan (Supervisor de Ventas, 5 años en el puesto, confirmado empleado de Raz y Cía): dedica **30–40% de su tiempo operativo** a validación, **20–30 min por orden**; afirma que reducir a **2 minutos** ya sería un éxito. Fuente: `Entregable 3/Transcripcion de Entrevista.docx:00:00:18` + `Entregable 3/2.2 User Persona...:Juan`.
* Encuesta n=27 (n=21 que sí gestionan órdenes): **76,2%** (16/21) responde “Sí / Claramente” a que el proceso podría ser más simple/rápido. Fuente: `Encuesta (Respuestas).xlsx` (ver `01-research/survey-results.md`).
* Evidencia real de matching (catálogo `lista_articulos.xlsx` 2.119 SKUs + 3 órdenes reales `OC_N_94325...`, `PEDIDO RAZ MONTE`, `WhatsApp Image`): **100% de las órdenes** no traen el código de cliente esperado y expresan cantidades de forma distinta.

## 3. Contexto organizacional

* **Empresa caso:** distribuidora de alimentos (Raz y Cía), con clientes tipo supermercados/almacenes que hacen pedidos recurrentes.
* **Usuarios directos:** empleados administrativos / facturación / logística que reciben, verifican y cargan órdenes. Perfil validado: 38% Administración, 19% Ventas, 14% Logística (encuesta).
* **Usuarios indirectos:** clientes de la empresa que generan las órdenes (no usan Parity directamente, pero determinan los formatos).
* **Comprador/pagador (hipótesis 02-product):** la empresa como organización que contrataría la licencia.

## 4. Solución propuesta (visión completa)

Flujo TO-BE definido en `Relevamiento y Descubrimiento/flujo_estandarizador_para_empleado.*`:

```
Orden llega (cualquier canal) → Extracción + Matcheo contra catálogo → Dashboard tipo Excel para revisión → Empleado confirma/corrige → Exportación 1-clic al formato de importación del sistema interno
```

* **Matcheo:** código exacto + código de barras (búsqueda en `codbarra`, `codbarra2`, `codbarra3` del catálogo). Tabla de mapeo `razón social / CUIT / sucursal → código cliente interno`.
* **Detección de ambigüedad:** marca, no resuelve automáticamente (principio “no reemplazar criterio humano”).
* **Exportación:** formato que exige el sistema interno de Raz y Cía (columnas `Código | Código Proveedor | Descripción | Unidades | ...` — ver `OC_N_94325_-_SUCURSAL_ROJAS.xlsx`).

## 5. Alcance MVP vs. visión

| Dentro MVP (priorizado por `Analisis/pain_points_a_mvp.md`) | Fuera / v2 | Explícitamente fuera |
|---|---|---|
| **PP5 Código de cliente** (prerrequisito técnico, score 19/20) | PP6 Cantidad por cliente/formato (caso por caso) | **PP4b Fotos borrosas** — viabilidad 1/5, OCR poco confiable. Solución hoy: pedir reenvío legible |
| **PP2 Matching producto por código exacto + barcode** (score 18, mayor frustración de Juan) | PP3 Conversión automática de unidades (requiere tabla aún no confirmada) | |
| **PP1 Detección (no resolución) de ambigüedad** | PP4a Texto libre no estructurado (parser simple futuro) | |

Decisión validada por matriz de evaluación de alternativas (`Benchmarking -Estudio de factibidad.xlsx`): Alternativa 3 (Parity) obtuvo **755 pts** vs. 640/595/440/410 de las otras 4 opciones, destacándose en *Alineación con el problema* (10/10) y *Tiempo de desarrollo* (9/20).

## 6. Métricas de éxito tentativas

* Reducción de tiempo por orden: 20–30 min → < 5 min (objetivo intermedio 2 min — cita de Juan).
* % de líneas matcheadas automáticamente sin intervención.
* % de ambigüedades detectadas vs. no detectadas (falsos negativos).
* Reducción de errores de facturación por código/cantidad equivocada.

## 7. Referencias cruzadas

* Detalle de priorización: `03-requirements/prioritization.md` y `Analisis/pain_points_a_mvp.md:38-73`
* Definición de MVP: `02-product/mvp-definition.md`
* Investigación completa: `01-research/` (user persona, journey, entrevistas, encuesta)
* Catálogo real: `07-domain-data/product-catalog.md` (2119 artículos)
* Órdenes reales: `07-domain-data/real-order-examples/` (3 ejemplos)
* Stack y arquitectura: `05-architecture/`
