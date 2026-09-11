---
title: "Arquitectura"
description: "Visión técnica de Parity."
---

# Arquitectura

Parity es un monolito modular simple, pensado para validar el flujo antes de escalar.

```
[Cliente Web] → [API Go] → [PostgreSQL]
                     → [Catálogo]
```

* **API Go:** orquesta validación, matching y persistencia. Sin colas en MVP.
* **PostgreSQL:** fuente durable de órdenes y catálogo.
* **React:** subida, tabla de revisión y exportación.
* **Docker:** empaquetado reproducible.

Decisiones clave se registran como ADRs en `architecture-decisions`.
