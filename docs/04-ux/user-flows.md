---
title: "Flujos de usuario"
description: "Cómo se usa Parity de punta a punta."
---

# Flujos de usuario

## Flujo principal

1. El usuario arrastra un Excel o PDF a la zona de carga.
2. La plataforma extrae líneas, valida estructura y cantidades.
3. El sistema cruza cada línea contra el catálogo por código o barra.
4. La tabla muestra resultados con estados y permite editar fallidos.
5. El usuario confirma y exporta en un clic.

## Estados de línea

| Estado | Color | Acción del usuario |
| --- | --- | --- |
| **Exacta** | Verde | Ninguna — lista para exportar. |
| **Ambigua** | Amarillo | Elegir entre candidatos sugeridos. |
| **Fallida** | Rojo | Corregir código o descripción. |

El objetivo es que el 80% de las líneas quede en verde sin intervención.
