# Diseño de API — Parity (`/api/v1`)

> Contratos del backend + decisiones de `architecture-decisions.md`.
> Base: Gin (CRUD/auth/matching) + handler stdlib solo para transferencia de archivos. Auth: Bearer JWT Supabase, rol en `app_metadata`.
> **Fecha:** 2026-09-11.

## Convenciones

- JSON; errores `{code, message}` (ej. `CLIENT_NOT_MAPPED`, `LINE_NEEDS_REVIEW`, `UPLOAD_TOO_LARGE`).
- Listados: `?q=&limit=&offset=` → `{data:[], total}` (convención propuesta, a revisión del equipo en construcción).
- Estados de línea: `ok | revisar | error | faltante` (ADR-010). `match_por`: `exacto | barra | manual | llm`.
- CORS restringido al origen Pages (ADR-013).
- Permisos: `empleado` = órdenes propias/área; `admin` = todo + catálogo + mapeos (middleware Go, ADR-003).

## Endpoints

| Método | Ruta | Qué hace | Notas |
|---|---|---|---|
| POST | `/orders/upload` (stdlib, streaming) | Recibe Excel (≤10MB) o PDF (tope a definir) por carga manual, guarda en Storage, crea `orders` + `order_lines` en `revisar` | Dispara pipeline: Excel→excelize; PDF→pdfcpu+texto+LLM (ADR-007/009). Sin ingesta automática en MVP (ADR-019) |
| GET | `/orders/:id` | Orden + líneas con estados y candidatos | Incluye `match_por` y candidatos[] por línea |
| PATCH | `/orders/:id/lines/:lineId` | Edita campos de una línea (manual o dropdown); si cambia descripción→artículo, el backend recalcula `codigo` y revalida estado | Regla código↔descripción del dashboard |
| POST | `/orders/:id/lines` | Agrega producto a la orden | Valida contra catálogo al crear |
| DELETE | `/orders/:id/lines/:lineId` | Quita línea | Log en `match_logs` |
| GET | `/orders/:id/export.xlsx` (stdlib) | Genera Excel formato sistema interno + log de validaciones | Solo si no hay `error` bloqueante; `revisar` no bloquea pero se advierte |
| GET | `/jobs/:id` | Estado del job async (polling "validando con IA…") | `pendiente | procesando | listo | fallido` |
| GET | `/catalog?q=&limit=&offset=` | Busca artículos (ILIKE + trigramas, para el dropdown con buscador) | Ordenamiento de candidatos: calibra equipo |
| GET/POST | `/clients/mappings` | Lista / crea mapeo CUIT→código (admin) | Prerrequisito de exportación |
| GET | `/healthz` | Salud del servicio | Para Render + CI |

## Auth (delegado a Supabase)

Login/refresh/password: `supabase-js` contra Supabase Auth directamente (el backend **no** implementa login). El backend solo valida (middleware Gin → JWKS) y autoriza por rol. Auto-registro con default `empleado` (admin promueve); emails vía Resend (ADR-016).
