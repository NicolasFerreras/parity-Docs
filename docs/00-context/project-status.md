---
title: "Project Status"
---

# Estado del Proyecto — Parity

> Documento público: estado del producto (qué existe, qué sigue), sin información de casos particulares ni del proceso académico.

## 1. Fase actual

Fin de relevamiento y descubrimiento → definición de producto y arquitectura. El problema está validado como real y doloroso (tiempo operativo perdido, 4 síntomas recurrentes, frustración media-alta, margen de mejora ampliamente reconocido) y el matching propuesto como viable con datos reales.

## 2. Qué está validado

* **Problema real:** formato heterogéneo, unidades distintas, duplicados por cambio de packaging y descripciones ambiguas aparecen con frecuencia en la operación diaria.
* **Costo:** decenas de minutos por orden; la ambigüedad es el síntoma más frecuente y los duplicados el más frustrante.
* **Viabilidad técnica:** catálogo con múltiples columnas de barcode + órdenes reales confirman que el matching exacto+barcode funciona; el mapeo de cliente por datos fiscales es factible.
* **Decisión explícita:** fotos ilegibles fuera del MVP (OCR poco confiable; se mantiene "pedir reenvío legible").

## 3. Próximos pasos

| Área | Estado | Siguiente |
|---|---|---|
| Contexto y research | Completos | Mantener actualizados |
| Producto (alcance, propuesta, MVP) | Definido | Refinar con uso real |
| Requisitos (priorización) | Grilla completa | Historias, criterios y backlog |
| UX (sistema, flujos, prototipo) | Definido | Wireframes y tests con usuarios |
| Arquitectura | Definida (18 ADRs) | Spikes: PDF real, LLM, trigramas |
| Desarrollo | Pendiente | Convenciones, testing, CI/CD |
| Datos de dominio | Pendiente | Formatos y catálogo sanitizado |
| Gestión | Pendiente | Roadmap, sprints, riesgos |

## 4. Riesgos y supuestos activos

* **Calidad de entrada:** si el cliente envía foto ilegible, el MVP no lo resuelve — flujo "pedir reenvío".
* **Tabla de conversión de unidades no confirmada:** depende de que exista mapeo por producto/cliente (stretch).
* **Pipeline LLM:** costo/latencia por orden y privacidad de datos comerciales a evaluar en spike.
* **Proyecto free en nube:** pausas por inactividad (mitigado con keep-alive) y retención de archivos acotada.

## 5. Decisiones vigentes

* Sin OCR en MVP; matching exacto antes que barcode; ambigüedad se detecta, no se adivina.
* Auth gestionado (no casero); monolito modular + capas; repos separados; dev local + prod en nube.
* Filas de origen LLM nacen en `revisar`; `ok` solo si idéntico a catálogo.
