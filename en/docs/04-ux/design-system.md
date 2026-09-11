---
title: "Design System"
description: "Parity base components."
---

# Design System

Parity uses a minimal system, designed for dense tables and fast reading.

## Components

* **Review table:** rows with code, description, quantity and state. Inline editable cells.
* **State badges:** `exact`, `ambiguous`, `failed` — color + text, never color alone.
* **Upload bar:** progress + line count.
* **Export button:** disabled until no failures remain.

## Palette

* Green `#03F07C` for exact and primary actions.
* Yellow for ambiguous, red for failed.
* Light background `#FFF9EC` for table contrast.

The system avoids modals and keeps everything in one view.
