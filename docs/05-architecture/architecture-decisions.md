# Decisiones de Arquitectura (ADRs) — Parity

> **Formato:** Problema → Alternativas → Decisión → Consecuencias (§9.3). Trazabilidad a las 19 decisiones deequipo relevadas por preguntas (2026-09-11).
> **Fecha:** 2026-09-11.

## ADR-001 — Gin + stdlib net/http

- **Problema:** framework HTTP para el backend Go.
- **Alternativas:** solo stdlib / solo Gin / Gin + stdlib.
- **Decisión (equipo):** Gin para CRUD, auth y matching; stdlib para upload/download streaming de archivos grandes.
- **Regla de uso (obligatoria):** todo route JSON va en Gin; el handler stdlib es un único endpoint dedicado a transferencia de archivos (streaming directo a Storage/tmp sin cargar en memoria). Nada de lógica de negocio en el handler stdlib.
- **Consecuencias:** dos estilos conviviendo; code review debe hacer cumplir la regla.

## ADR-002 — Goose para migraciones

- **Problema:** versionado del esquema PostgreSQL.
- **Alternativas:** golang-migrate / goose / SQL manual.
- **Decisión (equipo):** Goose (migraciones SQL versionadas, simple y embebible).
- **Consecuencias:** `migrations/*.sql` en repo backend; CI aplica `goose up` en staging/prod.

## ADR-003 — Supabase Auth (reversión de JWT propio)

- **Problema:** autenticación del MVP.
- **Alternativas:** sin auth / API key / JWT propio / Supabase Auth.
- **Decisión (equipo, reversión fundada):** Supabase Auth — auth casero concentra riesgo (hash, refresh, expiración); servicio probado es más seguro y confiable.
- **Diseño:** login vía `supabase-js` en React → token Bearer por request → middleware Gin valida firma contra JWKS de Supabase → rol desde `app_metadata` (`admin` | `empleado`) → RLS como segunda capa (el backend usa `service_role`, nunca exponerla al frontend).
- **Bootstrap:** primer admin sembrado a mano; en la entrega se definen credenciales provisorias con la distribuidora (cambio obligatorio posterior).
- **Consecuencias:** tabla `auth.users` en Supabase + espejo `public.profiles(id, rol, nombre)`; dev local requiere Supabase CLI en Docker (ADR-004).

## ADR-004 — Ambientes: dev 100% local, prod en nube día 1

- **Problema:** dónde corre cada ambiente.
- **Decisión (equipo):** desarrollo con BD + API + Auth 100% locales (Supabase CLI vía Docker + `go run` + `npm run dev`); producción en nube desde el día 1; a nube solo llega lo verificado.
- **Consecuencias:** `docker-compose.yml` de dev en repo backend; variables por ambiente (`.env.local` vs secrets de prod).

## ADR-005 — Nube: Supabase + Render

- **Problema:** proveedor y servicios de producción con presupuesto $0.
- **Alternativas:** Render todo / Railway $5 / Neon+Render / Supabase+Render.
- **Decisión (equipo):** Supabase (Postgres + Storage + Auth) + Render (API Go + frontend estático).
- **Condiciones:** Supabase se usa **solo** como PG + Storage + Auth (no se adoptan otros servicios sin ADR); free tier se pausa tras 1 semana sin uso → mitigación con ping semanal o reactivación manual antes de demos; web Render free duerme (~1 min wake, aceptado para MVP).
- **Consecuencias:** archivos de órdenes en Supabase Storage (bucket con políticas por rol); frontend estático con `VITE_API_URL` por ambiente.

## ADR-006 — Repos separados BE / FE

- **Problema:** layout de repositorios.
- **Decisión (equipo):** repos separados (Go+Goose+migrations / React+TS), versionado y CI independientes.
- **Consecuencias:** contratos API congelados en `api-design.md`; breaking changes requieren ADR.

## ADR-007 — Excel con excelize; PDF a la par con spike previo

- **Problema:** librerías de importación.
- **Decisión (equipo):** Excel → `excelize` (confirmado). PDF → `pdfcpu` (validar/desencriptar) + `ledongthuc/pdf` (extraer texto) **a la par desde el día 1**, con spike previo obligatorio contra `PEDIDO RAZ MONTE 18 AGO.pdf`.
- **Descartado con evidencia:** Gotenberg — verificado en gotenberg.dev: es API de *conversión* (Office/HTML→PDF), **sin extracción de texto**; sumaría Chromium+LibreOffice sin valor para el MVP. `unipdf` descartado por licencia comercial.
- **Consecuencias:** si el spike da NO, PDF cae a stretch (Excel primero) sin rediseño — el pipeline PDF es un módulo aislado (`internal/parser/pdf`).

## ADR-008 — Ambigüedad determinística: ILIKE + trigramas, decide el empleado

- **Problema:** cómo generar candidatos ante descripción ambigua.
- **Decisión (equipo):** texto aproximado (`ILIKE`) + similitud por trigramas (`pg_trgm`, tolera typos como "guaymayen"); el empleado elige entre candidatos.
- **Consecuencias:** extensión `pg_trgm` + índice GIN en `articles.descrip`; ordenamiento de candidatos lo calibra el equipo (no bloquea arquitectura).

## ADR-009 — LLM solo para PDF-tabla, pre-matching, filas a `revisar`

- **Problema:** librerías no reconstruyen tablas en PDF.
- **Decisión (equipo):** pipeline PDF: librería + LLM en paralelo → reconciliador toma el JSON del LLM para completar/corregir extracción → recién ahí matching. **Toda fila de origen LLM nace en estado `revisar`, nunca `ok`.** PDF-texto → flujo librería normal. Excel → sin LLM. Chat de WhatsApp → texto libre (stretch), fuera de este flujo.
- **Abierto (spike):** proveedor/modelo; evaluación de privacidad (CUITs y precios reales a un LLM externo); timeout/reintentos y fallback (librería sola + todo a `revisar`); costo por orden.
- **Consecuencias:** interfaz `LLMExtractor` (puerto) para no acoplar proveedor; arquitectura no fija modelo.

## ADR-010 — Máquina de 4 estados, `ok` binario exacto

- **Problema:** cuándo una línea es válida sin intervención.
- **Decisión (equipo):** `ok` **solo** si lo extraído es idéntico a BD (código + descripción + unidad, sin tocar nada). Cualquier modificación → `revisar`. Dato presente pero inválido → `error`. Dato ausente en origen → `faltante`.
- **Consecuencias:** casi no hay umbrales numéricos (ok es binario); queda solo ordenamiento de candidatos. Dashboard y API usan estos 4 estados en todas partes.

## ADR-011 — Sin OCR en MVP (fotos ilegibles fuera, heredado)

- **Problema:** fotos borrosas de WhatsApp.
- **Decisión (heredada de `project-status.md §5`, ratificada):** fuera por viabilidad 1/5; salida digna "ilegible — pedir reenvío legible".

## ADR-012 — Tipo: monolito modular + capas

- **Problema:** estilo arquitectónico del sistema.
- **Alternativas:** monolito modular / microservicios / serverless.
- **Decisión (equipo):** monolito modular + arquitectura por capas (Handler → Service → Repository).
- **Consecuencias:** un binario Go + SPA; microservicios solo por ADR futuro si la escala lo exige.

## ADR-013 — CORS restringido al origen Pages

- **Problema:** frontend y API en orígenes distintos (Pages vs Render).
- **Decisión (equipo):** CORS restringido al origen del frontend (sin proxy mismo-origen).
- **Consecuencias:** el origen permitido se configura por ambiente; documentar en deploy.

## ADR-014 — Trabajos async en PG + workers Go (sin Redis/Rabbit)

- **Problema:** concurrencia de importaciones con LLM (varios empleados a la vez).
- **Alternativas:** Redis + RabbitMQ (doc infra) / tabla `jobs` en PG + workers en el proceso Go.
- **Decisión (equipo, fundada §9.3):** PG + workers — el cuello es el LLM (segundos), no Go; a esta escala (2–5 concurrentes) un pool en-proceso + estados en PG da durabilidad y visibilidad sin salto de red, punto de falla ni secret extra.
- **Consecuencias:** tabla `jobs(id, order_id, estado, error, timestamps)`; dashboard hace polling de estado.

## ADR-015 — Retención: import efímero, export 14 días, SQL siempre

- **Problema:** Storage free 1GB (0,6MB/orden: 20 usuarios × 5/día × 14 días ≈ 840MB).
- **Decisión (equipo):** el importado se borra al procesar; el exportado vive 14 días vía `pg_cron` nocturno (verificado en free tier); registros SQL **siempre** (auditoría intacta).
- **Consecuencias:** buckets `ordenes/importadas/` + `ordenes/exportadas/`; `/healthz` toca PG para mantener activo el proyecto free.

## ADR-016 — Auto-registro con default `empleado` + SMTP Resend

- **Problema:** alta de usuarios y emails transaccionales.
- **Decisión (equipo):** auto-registro Supabase (default `empleado`, admin promueve desde dashboard); Resend como SMTP para bienvenida/registro.
- **Consecuencias:** `profiles.rol DEFAULT 'empleado'`; DSN Resend en secrets.

## ADR-017 — Sentry en MVP; Grafana en v2

- **Problema:** errores en producción y observabilidad.
- **Decisión (equipo):** Sentry (`sentry-go`, DSN en secrets) para panics/errores desde día 1; dashboards Grafana diferidos a v2 (Sentry + `/healthz` + métricas Render alcanzan).

## ADR-018 — Render Free + ping; secrets en env vars; sin staging

- **Problema:** tier, secretos y ambientes prod.
- **Decisión (equipo):** Render plan Free con UptimeRobot (ping cada menos de 15 min); secrets como env vars del servicio; sin staging (local + prod); dominios por defecto (`*.pages.dev`, `*.onrender.com`).
- **Consecuencias:** wake ~1min aceptado; si el sueño rompe demos, reabrir tier Starter por ADR.

## ADR-019 — Sin bot ni ingesta automática: MVP solo carga manual

- **Problema:** el flujo mencionaba "canal conectado: entra automático" heredado del SVG, y nunca se había registrado qué pasa con el bot de WhatsApp.
- **Decisión (equipo):** bot conversacional descartado + ingesta automática fuera del MVP. Única vía de entrada: carga manual (drag&drop / copy-paste / upload).
- **Consecuencias:** flujos y prototipo reflejan carga manual como única vía. Si a futuro se quiere ingesta automática, requiere ADR propio.
