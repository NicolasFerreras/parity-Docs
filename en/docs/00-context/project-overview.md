---
title: "Parity Documentation"
---

> Operational and product documentation for the Parity platform and its supporting infrastructure.

Parity is a purchase order standardizer for distributors: it receives orders exactly as each customer sends them (Excel, PDF, photo, text), automatically matches them against the internal catalog, and makes them available on a spreadsheet-style dashboard for human review in seconds. It combines a web application, a backend (API), and an extraction pipeline with LLM assistance for difficult cases.

This documentation is written for readers in product, operations, and engineering. It explains what Parity aims to achieve, how the core business workflows function, and how the technical system supports them.

## What Parity Does

Parity helps distributors:

* Receive orders in any format (Excel, PDF, text) without manual retyping.
* Automatically identify the customer (company name / CUIT → internal code).
* Match each line item against the catalog (exact code or barcode).
* Detect ambiguities and flag them for human review, without having to guess.
* Make corrections in an editable grid and export with a single click to the internal system’s format.

**Typical impact:** up to 30 minutes per order and a significant share of the workday spent on validation; most surveyed users believe the process could be simpler and faster.

##  Who it's for

* **Direct users:** admin, billing, logistics and sales employees who receive, verify and load orders.
* **Buyer:** the distributor as an organization (license).
* **Indirect users:** the customers who generate the orders (they don't use Parity, but they determine the formats).

## Main system components

| Component | Purpose |
|---|---|
| Web app | Signup, login, order upload and review dashboard. |
| API | Business backend and source of truth (orders, catalog, validations). |
| PostgreSQL | Durable source of truth. |
| Storage | Imported files (ephemeral) and exported files (14-day retention). |
| Managed auth | Signup, login and JWT tokens. |
| PDF + LLM pipeline | Extracts and structures PDF orders before matching. |
| Sentry | Production errors and crashes. |

## Documentation Map

* **Overview** explains the product logic, current status, and system architecture.
* **Product** explains the user lifecycle and order processing.
* **Design** explains UX/UI principles, the dashboard, and the visual system.
* **Technical** explains the platform, PDF pipeline, APIs, authentication, and data.
* **Operations** explains deployment, infrastructure, observability, and runbooks.
* **How We Work** explains the development process involving agents and human approvals.

##  Current stage

Parity is in the MVP foundation phase. Its architecture consists of a modular monolith for the API plus a single-page application (SPA), with managed services for the database, authentication, and hosting. The goal is to validate the core workflow (order enters → validated order exits) before implementing more complex infrastructure.
