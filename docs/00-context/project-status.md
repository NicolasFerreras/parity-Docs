---
title: "Estado del proyecto"
---

# Estado del Proyecto — Parity

> Documento público: estado del producto (qué existe, qué sigue), sin información de casos particulares ni del proceso académico.

## 1. Fase actual

**Documentación completa →Fase actual: Desarrollo** Toda la fase de definición está cerrada: requisitos, arquitectura, UX/UI, testing, entorno de desarrollo, infraestructura y deploy. El problema está validado como real y doloroso, el stack tecnológico está definido, y los 9 stubs restantes son de gestión/tracking (no bloquean el codeo).

## 2. Qué está validado

* **Problema real:** formato heterogéneo, unidades distintas, duplicados por cambio de packaging y descripciones ambiguas aparecen con frecuencia en la operación diaria.
* **Costo:** decenas de minutos por orden; la ambigüedad es el síntoma más frecuente y los duplicados el más frustrante.
* **Viabilidad técnica:** catálogo con múltiples columnas de barcode + órdenes reales confirman que el matching exacto+barcode funciona; el mapeo de cliente por datos fiscales es factible.
* **Decisión explícita:** fotos ilegibles fuera del MVP (OCR poco confiable; se mantiene "pedir reenvío legible").
* **Stack tecnológico:** Go + React/TypeScript + PostgreSQL. Backend en Render, frontend en Cloudflare Pages, DB + Auth + Storage en Supabase.
* **Requisitos:** 10 funcionales (R-001 a R-010), 5 no funcionales (R-NF01 a R-NF05), 10 reglas de negocio (RB-001 a RB-010).
* **User Stories:** 9 stories (US1 a US9) con criterios de aceptación Given/When/Then y priorización por grid F1-F9.
* **Arquitectura:** 18 ADRs, monolito modular (Handler → Service → Repository), repos separados (backend Go / frontend React).
* **Testing:** estrategia backend (150-200 tests, 4 cuadrantes) y frontend (24 tests FE-01 a FE-24) documentadas.
* **Entorno de desarrollo:** setup local con Docker (Supabase CLI), Makefile con comandos estandarizados, variables de entorno documentadas.
* **Deploy:** Render (backend) + Cloudflare Pages (frontend) + cron-job.org (keep-alive). CI/CD con GitHub Actions.

## 3. Próximos pasos

| Área | Estado | Siguiente |
|---|---|---|
| Contexto y research | ✅ Completos | Mantener actualizados |
| Producto (alcance, propuesta, MVP) | ✅ Definido | Refinar con uso real |
| Requisitos (historias, criterios, backlog) | ✅ Completos | Trazabilidad R→US→TC→Impl |
| UX (sistema, flujos, guidelines) | ✅ Definido | Wireframes y tests con usuarios |
| Arquitectura (18 ADRs, diagramas) | ✅ Definida | Spikes: PDF real, LLM, trigramas |
| Testing (backend + frontend) | ✅ Estrategia definida | Implementar tests según matriz |
| Entorno y deploy | ✅ Configurado | Primer setup local + CI/CD |
| Infraestructura y herramientas | ✅ Documentada | — |
| Datos de dominio | ✅ Formatos y catálogo | Sanitizar catálogo real para testing |
| Gestión (roadmap, sprints, riesgos) | ⏸️ Stubs pendientes | Completar mientras se desarrolla |
| **Desarrollo** | 🔜 **Fase actual** | Arrancar US1 (carga de orden Excel) |

## 4. Riesgos y supuestos activos

* **Calidad de entrada:** si el cliente envía foto ilegible, el MVP no lo resuelve — flujo "pedir reenvío".
* **Tabla de conversión de unidades no confirmada:** depende de que exista mapeo por producto/cliente (stretch).
* **Pipeline LLM:** costo/latencia por orden y privacidad de datos comerciales a evaluar en spike.
* **Proyecto free en nube:** pausas por inactividad (mitigado con keep-alive) y retención de archivos acotada.

## 5. Decisiones vigentes

* Sin OCR en MVP; matching exacto antes que barcode; ambigüedad se detecta, no se adivina.
* Auth gestionado (no casero)
* Monolito modular + capas; repos separados; dev local + staging + prod en nube.
* Filas de origen LLM nacen en `revisar`; `ok` solo si idéntico a catálogo.
