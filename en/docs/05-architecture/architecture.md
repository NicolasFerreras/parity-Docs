---
title: "Architecture"
description: "Technical vision of Parity."
---

# Architecture

Parity is a simple modular monolith, designed to validate the flow before scaling.

```
[Web Client] → [Go API] → [PostgreSQL]
                    → [Catalog]
```

* **Go API:** orchestrates validation, matching and persistence. No queues in MVP.
* **PostgreSQL:** durable source for orders and catalog.
* **React:** upload, review table and export.
* **Docker:** reproducible packaging.

Key decisions are recorded as ADRs in `architecture-decisions`.
