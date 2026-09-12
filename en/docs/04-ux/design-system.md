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

**Pending rules to define:**
- [ ] Safety area: _e.g. `x = height of the P` around it, 16px minimum in digital_
- [ ] Minimum size: _e.g. 24px isotype, 120px horizontal lockup_
- [ ] Isotype vs. lockup: when to use each (app bar vs. hero)
- Logotype font: **League Spartan** (confirmed for logo, not final for UI — see §3)

## 2. Palette

**Confirmed colors:**

| Token | HEX | Usage |
|---|---|---|
| `color-primary` | `#03F07C` | Main CTAs, validated highlight, success accent |
| `color-primary-soft` | `#5DE9AA` | Hover, "match ok" badges, subtle backgrounds, charts |
| `color-surface-warm` | `#FFF9EC` | Main light background (warm alternative to pure white) |
| `color-accent-amber` | `#D5A129` | Alerts, "review", warnings |
| `color-ink` | `#000000` | Main dark text, icons |

**Light / dark system (adaptive, not fixed):**

- **Light:** `bg: #FFF9EC` / `surface: #FFFFFF` / `ink: #000000` / `primary: #03F07C`
- **Dark:** `bg: #0A0A0A` (≈ black) / `surface: #1A1A1A` / `ink: #FFF9EC` / `primary: #03F07C` (keeps contrast)

**Pending complementary palette:** define 3 extra HEX if needed for states (error, info, disabled). Provisional proposal:
- `color-error: #E85D5D` / `color-info: #4A90E2` / `color-border: #E8E8E0` (to validate with visual direction).

## 3. Typography

**Logo:** League Spartan (confirmed, not mandatory for UI).

**Combination recommendation (proposal, not final):**
- **Option 1 (modern SaaS):** `Inter Display 500` (headings) + `Inter 400 / DM Sans 500` (body/UI) — safe, legible in dense tables.
- **Option 2 (editorial + tech):** serif display (hero) + `Inter 400` (body) + grotesque (CTAs/badges).
- **Option 3 (minimal single variable):** variable font for everything + tabular for data.

> Pending decision: pick the final combination and test on a dense Excel-like grid (number/code legibility). Document the final pair and weights here.

**Provisional scale:** `12 caption / 14 body / 16 ui / 20 h3 / 28 h2 / 40 h1` — 1.5 line height.

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
*Next: define complementary HEX + pick final type combination and document logo safety area when visual direction closes.*
