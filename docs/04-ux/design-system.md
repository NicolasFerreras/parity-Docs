---
title: "Diseño de sistema"
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

## 2. Paleta

**Colores confirmados:**

| Primary | `#059669` | Botones, links, acentos |
| --- | --- | --- |
| Secondary | `#10b981` | Gradientes, hover states |
| Button shadow | `#047857` | Borde/botón SpecularButton |
| Accent bright | `#5DE9AA` | Acentos Brillantes |
| Background | `#ffffff` | Fondo general |
| Text primary | `#0b1220` | Texto principal |
| Text secondary | `#6b7280` (gray-600) | Subtítulos, descripciones |
| Text muted | `#9ca3af` (gray-500) | Labels pequeños |
| Border | `#e5e7eb` (gray-200) | Bordes de secciones |

## 3. Tipografía

**Logo:** League Spartan (confirmada, no obligatoria para UI).

| **Fuente** | **Peso** | **Uso** |
| --- | --- | --- |
| **Inter** | 400 | Body, UI, texto general |
| **DM Sans** | 500 | Headings, CTAs, badges (`.font-grotesque`) |

| **Token** | **Tamaño** |
| --- | --- |
| Caption | `14px` |
| Body | `17px` |
| UI | `19px` |
| H3 | `24px` |
| H2 | `34px` |
| H1 | `48px` |

### **Altura de línea global**

- Body: `1.6`
- Headings: `1.3`
- Hero h1: `1.05`

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
