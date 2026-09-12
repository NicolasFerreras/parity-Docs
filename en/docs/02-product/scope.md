---
title: "Scope"
---

# Scope — Parity

> Public document. What enters the MVP, what is stretch and what is explicitly out, with pain traceability.

## 1. In the MVP (committed core)

| Feature | Pain it attacks | Basis |
|---|---|---|
| Customer code detection (business name/tax ID → code table) | Nothing loads without it (prerequisite) | Simple lookup table |
| Matching by exact code + barcode | Duplicates: top operational frustration | Confirmed with real data |
| Document import/export (validated structured Excel) | Cross-cutting | Parse/export + centralized storage |
| Ambiguity detection (not resolution) in descriptions | Ambiguity: most frequent symptom | Deterministic rules (approximate text + trigrams); LLM only as optional aid |

## 2. MVP stretch (conditional — team's risk call)

The team attempts everything below in the MVP, leaving only OCR out. If time runs short, **free text and/or ambiguity detection drop to v2 without compromising the rest**.

| Feature | Condition |
|---|---|
| Free-text order interpretation (mail/WhatsApp body) | Requires its own LLM pipeline |
| "Quantity" translation per customer format (cases/units/displays/packs) | Case by case per customer |
| Automatic unit conversion (loose vs. dozen) | Only if a conversion table is confirmed |
| Product and customer catalog browsing | Quick lookup panel |

**Rationale:** the prioritization grid scores each feature on value (research evidence) vs. effort (team estimate). An LLM pipeline's high cost is in building it the first time (prompts, model mistakes, per-order cost/latency, non-deterministic testing).

## 3. Explicitly out of the MVP

| Feature | Reason |
|---|---|
| OCR on blurry WhatsApp photos | Low viability; a non-technical fix exists (ask for legible resend) |

## 4. Pain → feature traceability

- **Missing customer code → customer detection** (no real order carries the expected code).
- **Duplicates → barcode matching** (solves packaging changes).
- **Ambiguity → detection** (flags, doesn't guess).
- **Per-customer quantity → quantity translation** (v2 case by case).
- **Unit conversion → automatic conversion** (needs unconfirmed table).
- **Free text → interpretation** (stretch); **blurry photo → out**.
