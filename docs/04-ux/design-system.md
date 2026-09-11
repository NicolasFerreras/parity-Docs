---
title: "Design System"
---

# Design System — Parity

> Identidad visual de Parity: logo dual + paleta confirmada + tipografía del logotipo. Estado: dirección visual de UI en investigación — aquí se documenta lo definido + pendientes explícitos.

## 1. Logo

| Elemento | Uso |
|---|---|
| **Isotipo (sin nombre)** | Favicon, avatar, loading, marca de agua, ícono app |
| **Principal fondo claro** (letras negras) | Header, hero, docs con fondo `#FFF9EC` / blanco |
| **Principal fondo oscuro** (letras blancas) | Header dark mode, splash oscuro, slides |
| **Variantes fondo sólido** (blanco / negro) | Cuando no se puede usar transparencia (mail, PDF) |
| **Lockup final** | Master para imprenta / presentación |

**Reglas pendientes por definir:**
- [ ] Área de seguridad: _ej. `x = altura de la P` alrededor, mínimo 16px en digital_
- [ ] Tamaño mínimo: _ej. 24px isotipo, 120px lockup horizontal_
- [ ] Isotipo vs. lockup: cuándo usar cada uno (app bar vs. hero)
- Fuente del logotipo: **League Spartan** (confirmada para logo, no definitiva para UI — ver §3)

## 2. Paleta

**Colores confirmados:**

| Token | HEX | Uso |
|---|---|---|
| `color-primary` | `#03F07C` | CTAs principales, highlight validado, acento éxito |
| `color-primary-soft` | `#5DE9AA` | Hover, badges “match ok”, fondos sutiles, gráficos |
| `color-surface-warm` | `#FFF9EC` | Fondo claro principal (alternativa a blanco puro, cálido) |
| `color-accent-amber` | `#D5A129` | Alertas, “revisar”, warnings |
| `color-ink` | `#000000` | Texto principal dark, íconos |

**Sistema light / dark (adaptativo, no fijo):**

- **Light:** `bg: #FFF9EC` / `surface: #FFFFFF` / `ink: #000000` / `primary: #03F07C`
- **Dark:** `bg: #0A0A0A` (≈ negro) / `surface: #1A1A1A` / `ink: #FFF9EC` / `primary: #03F07C` (mantiene contraste)

**Paleta complementaria pendiente:** definir 3 HEX adicionales si se necesitan para estados (error, info, disabled). Propuesta provisional:
- `color-error: #E85D5D` / `color-info: #4A90E2` / `color-border: #E8E8E0` (a validar con dirección visual).

## 3. Tipografía

**Logo:** League Spartan (confirmada, no obligatoria para UI).

**Recomendación de combinación (propuesta, no definitiva):**
- **Opción 1 (SaaS moderna):** `Inter Display 500` (headings) + `Inter 400 / DM Sans 500` (body/UI) — segura, legible en tablas densas.
- **Opción 2 (Editorial + tech):** display serif (hero) + `Inter 400` (body) + grotesca (CTAs/badges).
- **Opción 3 (Variable única, minimal):** variable para todo + tabular para datos.

> Decisión pendiente: elegir combinación final y testear en grilla Excel densa (legibilidad números/códigos). Documentar aquí el par final y pesos.

**Escala provisional:** `12 caption / 14 body / 16 ui / 20 h3 / 28 h2 / 40 h1` — inter 1.5.

## 4. Dirección visual

Estado: **en investigación**.

- **Queremos transmitir:** Una tecnología moderna, precisa y confiable.
- **Estilo:** Minimalista · SaaS · Moderno · Profesional · Tecnológico · Limpio
- **Referencias visuales:** _[pendiente — agregar 2-3 productos referencia cuando se defina dirección]_
- **Tokens visuales a explorar:** bordes suaves (rx 8), sombras ligeras, grilla densa tipo spreadsheet, badges semánticos (verde ok, ámbar revisar, rojo error).

## 5. Componentes base (MVP)

**Grilla tipo Excel (dashboard corazón):**
- Columnas de orden (`Código | Código Proveedor | Descripción | Proveedor | Unidades | Display | U.Compra | Costo U. | Total`) + col. `Estado` (ok/revisar/error/faltante) con icono.
- Celdas editables inline, validación en línea, tooltip de alternativa.
- Fila duda → fondo `#FFF9EC` + borde `#D5A129` + badge “Revisar”.

**Estados de validación:**
- **ok** — fondo `#03F07C` texto `#000000` / **revisar** — `#D5A129` / **error** — `color-error` / **faltante** — gris.

**CTAs:**
- Primario: `Exportar a Excel — 1 clic, listo para enviar` (verde `#03F07C`) / Secundario: “Corregir la orden — edición tipo Excel”

**Otros:** uploader drag&drop, mapeo cliente (CUIT/razón social → código), tolerancia a formatos heredados.

---
*Próximo: definir HEX complementarios + elegir combinación tipográfica final y documentar área seguridad logo cuando dirección visual cierre.*
