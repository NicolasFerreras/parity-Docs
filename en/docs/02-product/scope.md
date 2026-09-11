---
title: "Scope"
description: "What Parity includes and excludes in its initial version."
---

# Scope

Parity covers the complete flow from order reception to final validation, without replacing the client's existing systems.

## In Scope

* Excel and PDF ingestion with line extraction.
* Structure, quantity and code validation.
* Matching by internal code and barcode against catalog.
* Human review of ambiguous or failed cases in the web interface.
* One-click export to the internal format.

## Out of Scope (MVP)

* Blurry photo or audio processing.
* Automatic price or promotion calculation.
* Direct ERP billing integration.
* Asynchronous processing with queues or microservices.

The goal is to validate the core flow with minimal infrastructure before scaling.
