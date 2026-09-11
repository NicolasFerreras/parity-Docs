# Estado del Proyecto — Parity (2026-09-07)

> Corte al 07/09/2026. Fuentes: `Documentacion de proyecto/Resumen.txt`, `Analisis/pain_points_a_mvp.md`, `Clases/*`, `01-research/*`.

## 1. Fase actual

**Fin de etapa de Relevamiento y Descubrimiento → inicio de definición de producto / arquitectura.**

Checklist de entregables académicos:

| Entregable | Estado | Evidencia |
|---|---|---|
| Formulación inicial (Template V1.2) | ✅ Entregado 19/08 | `Relevamiento y Descubrimiento/1.2.Template...docx` |
| Matriz de evaluación de alternativas / Estudio de factibilidad | ✅ 25–28/08 | `1.1. Benchmarking -Estudio de factibidad.xlsx` — Alternativa 3 (Parity) ganadora con 755 pts |
| Guía de entrevista + Encuesta | ✅ 25–28/08 | `Analisis/Entregable 2/Guía de Entrevista...` + `Encuesta alternativa.docx` (10 preguntas, lógica de salto) |
| User Persona + Mapa de Empatía **preliminar** (versión “Rocío”, 33a) | ✅ 28/08 | `Entregable 2/2.4.Estudio de mercado.docx:User Persona preliminar` — etiquetado HECHO/HIPÓTESIS |
| Ejecución: encuesta n=27 + entrevista a Juan | ✅ 01/09 | `Encuesta (Respuestas).xlsx` + `Transcripcion de Entrevista.docx` (audio IA + revisión manual) |
| User Persona + Mapa + Journey **validados** (versión “Juan”, 30a, Supervisor) | ✅ 04/09 | `Entregable 3/2.2 User Persona...docx` + `3.Estudio de mercado (mapas).docx` |
| Documento `De los Pain Points al MVP` | ✅ 03/09 | `Analisis/pain_points_a_mvp.md` — 6 pain points priorizados, MVP definido |
| Documento de marca / logos “Parity” | ✅ | `Diseño UX-UI/Documento de marca.docx` + `Logo + nombre final.pdf` (6 variantes PNG) |
| Flujo estandarizador (png/svg) | ✅ | `Relevamiento y Descubrimiento/flujo_estandarizador_para_empleado.*` |

## 2. Qué está validado

* **Problema es real y doloroso:** entrevista confirma 30–40% tiempo operativo, 4 síntomas recurrentes; encuesta (21 que gestionan OC) muestra: formato “frecuentemente/siempre” 19% + “a veces” 43%; unidad 24% frec./siempre; duplicados 33% frec./siempre; ambigüedad 43% frec./siempre (síntoma más reportado).
* **Frustración:** promedio 3,6/5 (9×4, 7×3, 2×5). 76% cree que puede ser más simple (10×Sí + 6×Claramente).
* **Matching es viable con datos reales:** cruce catálogo (2119 SKUs, 3 columnas barcode) + 3 órdenes reales confirma que búsqueda por barcode resuelve PP2; mapeo CUIT/razón social → código cliente resuelve PP5.
* **Riesgos descartados conscientemente:** PP4b (fotos borrosas) fuera de MVP por viabilidad 1/5 — decisión explícita docente-criterio impacto+frecuencia+riesgo+viabilidad.

## 3. Qué falta / próximos pasos (roadmap académico)

| Área docs | Estado actual en `docs/` | Siguiente paso |
|---|---|---|
| `00-context` | vacío antes de este commit (0 chars) — ahora completo | Mantener actualizado |
| `01-research` | vacío — ahora completo con evidencia | Revisión cruzada con docentes |
| `02-product` (scope, value prop, BMC, MVP) | vacío — pendiente | Migrar `pain_points_a_mvp.md` + `Clase 4 Canvas` a `02-product/` |
| `03-requirements` | placeholders (6 archivos con TODO) | Transformar PPs → user stories + criterios de aceptación |
| `04-ux` | placeholders | Wireframes del dashboard tipo Excel + flujo estandarizador |
| `05-architecture` | placeholders | Modelo de dominio (catálogo, OC, cliente, mapeos), ER, decisiones |
| `06-development` | placeholders | Definir git workflow, convenciones, testing |
| `07-domain-data` | vacío + .gitkeep — ahora poblado | Copiar `lista_articulos.xlsx` (catálogo anonimizado) y 3 OCs de `Informacion de apoyo/` |
| `08-project-management` | placeholders | Roadmap v2, sprints, riesgos |

## 4. Riesgos y supuestos activos

* **Muestra encuesta general, no solo distribuidora de alimentos:** 21 respuestas son de rubros variados (validado en `pain_points_a_mvp.md:6` — “porcentajes reflejan problema en rubro en general”). Mitigación: entrevista Juan + evidencia real de matching son la validación específica.
* **Acceso limitado a stakeholders:** solo 1 entrevista en profundidad (Juan) vs. objetivo 3–5. Mitigación: ampliar entrevistas antes de cerrar requirements.
* **Tabla de conversión de unidades (PP3/PP6) no confirmada:** depende de que exista mapeo por producto/cliente.
* **Dependencia de calidad de datos de entrada:** si cliente envía foto borrosa, Parity no resuelve en MVP — flujo alternativo “pedir reenvío” (ya usado hoy).

## 5. Decisiones recientes (ADRs tempranos)

* **No OCR en MVP:** pp4b fuera por viabilidad baja (Clase 3 criterio viabilidad).
* **Matching primero por código exacto, luego barcode:** confirmado con datos reales, viabilidad 5/5.
* **Detección, no resolución automática de ambigüedad:** respeta principio “no reemplazar criterio humano” (`Resumen.txt:12`).

## 6. Métrica de avance docs

* `docs/00-context` y `docs/01-research` (9 archivos) — **completados** en este corte (2026-09-07).
* `docs/02-product` → `08-project-management` — **pendientes**, con fuentes ya relevadas.

---

*Actualizado por: documentación sintetizada desde `Entregables facu/` (excluyendo `agentes/` y `Prompt agente`). Próximo hito: completar `02-product/` y `03-requirements/`.*
