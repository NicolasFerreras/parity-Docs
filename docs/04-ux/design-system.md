---
title: "Sistema de diseño"
description: "Componentes base de Parity."
---

# Sistema de diseño

Parity usa un sistema mínimo, pensado para tablas densas y lectura rápida.

## Componentes

* **Tabla de revisión:** filas con código, descripción, cantidad y estado. Celdas editables inline.
* **Badges de estado:** `exacta`, `ambigua`, `fallida` — color + texto, nunca solo color.
* **Barra de carga:** progreso + conteo de líneas procesadas.
* **Botón de exportación:** deshabilitado hasta que no haya fallidos.

## Paleta

* Verde `#03F07C` para exactas y acciones primarias.
* Amarillo para ambiguas, rojo para fallidas.
* Fondo claro `#FFF9EC` para contraste en tablas.

El sistema evita modales y mantiene todo en una vista.
