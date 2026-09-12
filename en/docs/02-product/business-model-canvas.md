---
title: "Business Model Canvas"
---

# Business Model Canvas — Parity

> Public document. 9-block business model.

## 1. Customer segments

| Segment | Detail |
|---|---|
| **Direct users** | Admin, billing, logistics and sales employees who receive, verify and load orders. |
| **Buyer** | The distributor as an organization (license). Hypothesis to validate commercially. |
| **Indirect users** | The customers who generate the orders (they don't use Parity, but they determine the formats). |

## 2. Value proposition

**Messy order in, validated order out. No re-typing, no hidden doubts, with human control to the end.**

- Turns heterogeneous orders (WhatsApp, mail, PDF, Excel, photo) into a catalog-validated spreadsheet in seconds.
- Doesn't replace the employee — it assists: it flags the ambiguous instead of guessing.
- Details: `value-proposition.md`.

## 3. Channels

- **Input:** WhatsApp, email, PDF, Excel, plain text, photo — manual upload only in MVP.
- **Delivery:** Excel-like dashboard + 1-click export to the internal system format.
- **Commercial (hypothesis):** direct sale to distributors.

## 4. Customer relationships

- **Assistance, not replacement:** the user has the last word.
- **Visible traceability:** every row says how it was matched (exact code / barcode / manual) — builds trust.
- **Learning by use:** corrections feed per-customer equivalences (v2).

## 5. Revenue streams (to define)

- Hypotheses to evaluate: per-company license (SaaS) and/or per-order volume.
- No pricing model until validated with decision makers.

## 6. Key resources

- Internal catalog (thousands of SKUs, multiple barcode columns).
- Customer mapping table (business name / tax ID / branch → internal code) — prerequisite.
- Matching engine (exact code → barcode → ambiguity detection).
- Document parser and importer/exporter.

## 7. Key activities

1. Extract products and quantities from any input format.
2. Match against catalog and map customer.
3. Flag ambiguity and duplicates for human review.
4. Export to internal format + validation log (auditing).

## 8. Key partners

- Distributors validating domain and real data.
- Product team + instructors (impact + frequency + risk + viability criteria).

## 9. Cost structure (to define)

- Top known cost: building the text-interpretation pipeline the first time (prompts, model mistakes, per-order cost/latency, non-deterministic testing).
- Minimal infra: managed database, storage and hosting services.
