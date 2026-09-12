---
title: "Project Overview"
---

# Project Overview — Parity

> Public document. Universal B2B tone: describes the product for any distributor, with no case-specific data.

## 1. Elevator pitch

**Parity — Purchase Order Standardization**. Parity receives the purchase order exactly as the customer sends it (WhatsApp, email, PDF, Excel, photo), interprets it automatically against the internal catalog, and leaves it ready on an Excel-like dashboard for human review in **seconds**, not tens of minutes. It does not replace the employee: **it assists** — when something is ambiguous, it flags it for a decision.

## 2. Problem

At a distributor, receiving and loading orders requires a fixed format (`product code + description + quantity`), but:

* Orders arrive through **multiple channels** with no single format (WhatsApp, email, PDF, Excel, photos).
* Each customer uses **their own codes, their own way of describing products, and their own quantity logic** (boxes, units, displays, packs).
* Today an employee translates everything **by hand**: looking up which product each code maps to, fixing units, resolving ambiguities by personal criteria.

**Typical impact:** up to 30 minutes per order and a significant share of the workday spent on validation; most surveyed users believe the process could be simpler and faster.

## 3. Who it's for

* **Direct users:** admin, billing, logistics and sales employees who receive, verify and load orders.
* **Buyer:** the distributor as an organization (license).
* **Indirect users:** the customers who generate the orders (they don't use Parity, but they determine the formats).

## 4. Proposed solution (TO-BE flow)

```
Order arrives (any channel) → Extraction + Matching against catalog → Excel-like dashboard for review → Employee confirms/corrects → 1-click export to the internal system's format
```

* **Matching:** exact code + barcode (up to 3 EANs per product). Mapping table `business name / tax ID / branch → internal customer code`.
* **Ambiguity detection:** flagged, never auto-resolved ("don't replace human judgment" principle).
* **Export:** internal system import format + validation log for auditing.

## 5. Main system components

| Component | Purpose |
|---|---|
| Web app | Signup, login, order upload and review dashboard. |
| API | Business backend and source of truth (orders, catalog, validations). |
| PostgreSQL | Durable source of truth. |
| Storage | Imported files (ephemeral) and exported files (14-day retention). |
| Managed auth | Signup, login and JWT tokens. |
| PDF + LLM pipeline | Extracts and structures PDF orders before matching. |
| Sentry | Production errors and crashes. |

## 6. MVP scope vs. vision

| In the MVP | Stretch (if time allows) | Explicitly out |
|---|---|---|
| Customer code detection (prerequisite: no export without it) | Free text (requires its own LLM pipeline) | OCR on illegible photos (graceful exit: ask for legible resend) |
| Matching by exact code + barcodes | Per-customer quantities, unit conversion | |
| Document import/export | Catalog browsing | |
| Ambiguity detection (not resolution) | | |

## 7. Success metrics

* Time per order: tens of minutes → under 5 (target 2).
* % of lines auto-matched with no intervention.
* % of ambiguities detected vs. missed (false negatives).
* Fewer billing errors from wrong code/quantity.

## 8. Current stage

MVP foundation phase: modular monolith + SPA with managed services. Goal: validate the core loop (order in → validated order out) before heavier infrastructure. Details in `project-status.md`.
