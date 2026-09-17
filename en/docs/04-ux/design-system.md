---
title: "Design System"
---

# Design System — Parity

> Parity's visual identity: dual logo + confirmed palette + logotype typography. Status: UI visual direction under research — here is what's defined + explicit placeholders.

## 1. Logo

| Element | Usage |
|---|---|
| **Isotype (no name)** | Favicon, avatar, loading, watermark, app icon |
| **Light-background primary** (black letters) | Header, hero, docs on `#FFF9EC` / white |
| **Dark-background primary** (white letters) | Dark-mode header, dark splash, slides |
| **Solid-background variants** (white / black) | When transparency is unusable (mail, PDF) |
| **Final lockup** | Master for print / presentations |

## 2. Palette

**Confirmed colors:**

| Primary | \`#059669\` | Buttons, links, accents |
| --- | --- | --- |
| Secondary | \`#10b981\` | Gradients, hover states |
| Button shadow | \`#047857\` | Border/SpecularButton |
| Accent bright | \`#5DE9AA\` | Bright accents |
| Background | \`#ffffff\` | General background |
| Text primary | \`#0b1220\` | Main text |
| Text secondary | \`#6b7280\` (gray-600) | Subtitles, descriptions |
| Text muted | \`#9ca3af\` (gray-500) | Small labels |
| Border | \`#e5e7eb\` (gray-200) | Section borders |

## 3. Typography

**Logo:** League Spartan (confirmed, not mandatory for UI).

| **Typography** | **Weight** | **Use** |
| --- | --- | --- |
| **Inter** | 400 | Body, UI, text |
| **DM Sans** | 500 | Headings, CTAs, badges (`.font-grotesque`) |

| **Token** | **Size** |
| --- | --- |
| Caption | `14px` |
| Body | `17px` |
| UI | `19px` |
| H3 | `24px` |
| H2 | `34px` |
| H1 | `48px` |

### **Line-height global**

- Body: `1.6`
- Headings: `1.3`
- Hero h1: `1.05`

## 4. Visual direction

Status: **under research**.

- **We want to convey:** modern, precise, reliable technology.
- **Style:** Minimalist · SaaS · Modern · Professional · Technological · Clean
- **Visual references:** _[pending — add 2-3 reference products when direction is set]_
- **Visual tokens to explore:** soft borders (rx 8), light shadows, dense spreadsheet-like grid, semantic badges (green ok, amber review, red error).

## 5. Base components (MVP)

**Excel-like grid (core dashboard):**
- Order columns (`Código | Código Proveedor | Descripción | Proveedor | Unidades | Display | U.Compra | Costo U. | Total`) + `Estado` column (ok/revisar/error/faltante) with icon.
- Inline editable cells, inline validation, alternative tooltip.
- Doubt row → `#FFF9EC` background + `#D5A129` border + "Revisar" badge.

**Validation states:**
- **ok** — `#03F07C` background, `#000000` text / **revisar** — `#D5A129` / **error** — `color-error` / **faltante** — gray.

**CTAs:**
- Primary: `Export to Excel — 1 click, ready to send` (green `#03F07C`) / Secondary: "Fix the order — Excel-like editing"

**Other:** drag&drop uploader, customer mapping (tax ID/business name → code), tolerance for legacy formats.

---
