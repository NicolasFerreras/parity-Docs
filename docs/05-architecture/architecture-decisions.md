---
title: "Architecture Decisions"
---

# Decisiones de Arquitectura — Parity

> Lista de decisiones vigentes. Cada una sigue Problema → Alternativas → Decisión → Consecuencias. Trazabilidad a decisiones de equipo relevadas.
> **Fecha:** 2026-09-11.

- **Framework HTTP (Gin + stdlib):** Gin para CRUD, auth y matching; stdlib solo para upload/download por streaming. Regla obligatoria: nada de lógica de negocio en el handler de archivos.
- **Migraciones (Goose):** esquema versionado en SQL; CI aplica `goose up` en prod.
- **Auth gestionado (Supabase Auth):** reversión fundada de JWT propio (auth casero concentra riesgo). Login con librería cliente, backend valida firma y autoriza por rol (`admin` | `empleado`); RLS como segunda capa. Primer admin sembrado a mano.
- **Ambientes (dev local, prod nube día 1):** desarrollo 100% local con stack en Docker; a nube solo llega lo verificado.
- **Nube (Supabase + Render):** Supabase como Postgres + Storage + Auth; Render como API + frontend. Solo esos usos sin nueva decisión. Proyecto free con keep-alive.
- **Repos separados:** backend Go + migraciones por un lado, frontend React por otro, con contratos de API congelados.
- **Excel (excelize) y PDF a la par:** Excel con librería estándar; PDF con validador + extractor de texto, con spike previo obligatorio contra un PDF real. Gotenberg descartado (es conversión, no extracción); `unipdf` descartado por licencia comercial.
- **Ambigüedad determinística:** candidatos por texto aproximado + trigramas (`pg_trgm`); el empleado elige, el sistema nunca elige solo.
- **LLM solo para PDF con tablas:** corre en paralelo a la librería antes del matching; el JSON completa o corrige la extracción. Toda fila de origen LLM nace en `revisar`. Proveedor, timeouts y privacidad a definir en spike. Excel sin LLM.
- **4 estados, ok binario:** `ok` solo si idéntico a catálogo; cualquier retoque → `revisar`; dato inválido → `error`; dato ausente → `faltante`.
- **Sin OCR en MVP:** fotos ilegibles fuera; salida digna "pedir reenvío legible".
- **Tipo (monolito modular + capas):** Handler → Service → Repository en un binario Go + SPA. Microservicios solo por decisión futura.
- **CORS restringido:** solo al origen del frontend, configurado por ambiente.
- **Async sin Redis ni Rabbit:** tabla de jobs en PG + workers en el proceso (el cuello es el LLM, no Go). Dashboard con polling de estado.
- **Retención:** importado efímero (se borra al procesar), exportado 14 días por tarea nocturna, registros SQL siempre (auditoría).
- **Registro y SMTP:** auto-registro con rol base operador (admin promueve) + Resend para emails de bienvenida.
- **Errores y observabilidad:** Sentry desde día 1; dashboards propios en v2.
- **Tier y secretos:** plan gratuito con ping keep-alive; secretos en variables del servicio; sin staging (local + prod); dominios por defecto.
- **Sin bot ni ingesta automática:** bot conversacional descartado; MVP solo carga manual. La ingesta automática futura requiere decisión propia.
