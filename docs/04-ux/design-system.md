# Design System — Parity

> **Origen:** `Diseño UX-UI/Documento de marca.docx:9` Identidad visual + `Logo + nombre final.pdf` + 6 PNGs (90–1022KB) + respuestas 2026-09-07 (paleta #03F07C etc., tipografías, logo dual). Estado: dirección visual en investigación — aquí se documenta lo definido + placeholders explícitos.

## 1. Logo

| Elemento | Archivo | Uso |
|---|---|---|
| **Isotipo (sin nombre)** | `Logo.png` (1022KB) | Favicon, avatar, loading, marca de agua, ícono app |
| **Principal fondo claro** | `Logo parity (sin fondo letras negras).png` (62KB) | Header, hero, docs con fondo `#FFF9EC` / blanco |
| **Principal fondo oscuro** | `Logo parity (sin fondo letras blancas).png` (48KB) | Header dark mode, splash oscuro, slides |
| **Variantes fondo sólido** | `Logo parity (fondo blanco).png` (90KB) / `(fondo negro).png` (85KB) | Cuando no se puede usar transparencia (mail, PDF) |
| **Variantes tipográficas** | `Parity letra negra.png` (41KB) / `Parity letras negras.png` (52KB) | Lockups alternos (evaluar cuál es principal tipográfico) |
| **Lockup final** | `Logo + nombre final.pdf` (1250KB) | Master para imprenta / presentación |

**Reglas pendientes por definir en `Documento:103-107`:**
- [ ] Área de seguridad: _ej. `x = altura de la P` alrededor, mínimo 16px en digital_
- [ ] Tamaño mínimo: _ej. 24px isotipo, 120px lockup horizontal_
- [ ] Isotipo vs. lockup: cuándo usar cada uno (app bar vs. hero)
- Fuente del logotipo: **League Spartan** (confirmada para logo, no definitiva para UI — ver §3)

> Ubicación física: `Entregables facu/Documentacion de proyecto/Diseño UX-UI/` — copiar a `07-domain-data/reference-files/branding/` para trazabilidad al implementar.

## 2. Paleta

**Colores confirmados 2026-09-07** (`Documento:109-118` `[HEX]`):

| Token | HEX | Origen | Uso |
|---|---|---|---|
| `color-primary` | `#03F07C` | Logo — primario | CTAs principales, highlight validado, acento éxito |
| `color-primary-soft` | `#5DE9AA` | Logo — secundario | Hover, badges “match ok”, fondos sutiles, gráficos |
| `color-surface-warm` | `#FFF9EC` | — | Fondo claro principal (alternativa a blanco puro, cálido) |
| `color-accent-amber` | `#D5A129` | — | Alertas, “revisar”, precios/condiciones dudosas, warnings |
| `color-ink` | `#000000` | — | Texto principal dark, íconos |

**Sistema light / dark (adaptativo, no fijo):**

- **Light:** `bg: #FFF9EC` / `surface: #FFFFFF` / `ink: #000000` / `primary: #03F07C` / `muted: #5DE9AA2A`
- **Dark:** `bg: #0A0A0A` (≈ negro) / `surface: #1A1A1A` / `ink: #FFF9EC` / `primary: #03F07C` (mantiene contraste AAA) / `muted: #5DE9AA20`

> Nota: paleta sujeta a cambio según dirección visual final. Los dos primeros HEX son de logo, por tanto inmutables salvo rebrand. Resto son tokens de trabajo.

**Paleta complementaria pendiente `Documento:115-118`:** definir 3 HEX adicionales si se necesitan para estados (error, info, disabled). Propuesta provisional:
- `color-error: #E85D5D` / `color-info: #4A90E2` / `color-border: #E8E8E0` (a validar con dirección visual).

## 3. Tipografía

**Logo:** League Spartan (confirmada, no obligatoria para UI).

**Opciones UI propuestas (max 3, óptimo 2 — `Documento:120-121` `[Fuente]`):**
InterVariable 500 · arizonaFlare 400 · Haffer XH 400 · Host Grotesk 600 · Inter 400 · Google Sans Flex Variable 400 · ivyPrestoHeadline 300 · Tobias 100 · Matter 360 · DM Sans 500 · Inter Display 500

**Recomendación de combinación (propuesta, no definitiva):**
- **Opción 1 (SaaS moderna, dual):** `Inter Display 500` (headings) + `Inter 400 / DM Sans 500` (body/UI) — segura, legible en tablas densas.
- **Opción 2 (Editorial + tech, triple si aporta contraste):** `ivyPrestoHeadline 300` (hero display) + `Inter 400` (body) + `Host Grotesk 600` (CTAs/badges).
- **Opción 3 (Variable única, minimal):** `Google Sans Flex Variable 400` (todo, jugando con opsz/wght) + `InterVariable 500` (datos tabulares).

> Decisión pendiente: elegir 1 combinación de las 11 listadas y testear en grilla Excel densa ( legibilidad números/codbarra). Documentar aquí el par final y pesos.

**Escala provisional:** `12 caption / 14 body / 16 ui / 20 h3 / 28 h2 / 40 h1` — inter 1.5.

## 4. Dirección visual

Estado: **en investigación** (`Documento:123-133`).

- **Queremos transmitir:** Una tecnología moderna, precisa y confiable. (`Documento:124` confirmado)
- **Estilo:** Minimalista · SaaS · Moderno · Profesional · Tecnológico · Limpio (`Documento:128-133`)
- **Referencias visuales `Documento:126`:** _[pendiente — agregar 2-3 links/imágenes de productos referencia cuando se defina dirección]_
- **Tokens visuales a explorar:** bordes 2xl suaves (rx 8), sombras ligeras, grilla densa tipo spreadsheet, badges semánticos (verde `#03F07C` ok, ámbar `#D5A129` revisar, rojo error).

## 5. Componentes base (MVP)

**Grilla tipo Excel (dashboard corazón):**
- Columnas espejo `OC_N_94325` (`Código | Código Proveedor | Descripción | Proveedor | Unidades | Display | U.Compra | Costo U. | Total`) + col. `Estado` (ok/duda/error) con icono.
- Celdas editables inline, validación en línea, tooltip de alternativa (ej. “EAN 7622210... también es 5271”).
- Fila duda → fondo `#FFF9EC` + borde `#D5A129` + badge “Revisar”.

**Estados de validación:**
- **ok** — fondo `#03F07C` texto `#000000` / **revisar** — `#D5A129` / **error** — `color-error` / **vacío** — gris.

**CTAs:**
- Primario: `Exportar a Excel — 1 clic, listo para enviar` (verde `#03F07C` sobre `surface`, `flujo.svg: Exportar a Excel`) / Secundario: “Corregir la orden — edición tipo Excel”

**Otros:** uploader drag&drop (WhatsApp/mail/PDF/foto), mapeo cliente (CUIT/razón social → código), tolerancia a formatos heredados.

---
*Próximo: definir HEX complementarios + elegir combinación tipográfica final y documentar área seguridad logo cuando dirección visual cierre.*
