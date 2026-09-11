# Definición de MVP — Parity

> Documento público. Qué debe cumplir el MVP, qué hipótesis valida y qué riesgos asume.

## 1. Enunciado del MVP

Probar que una orden heterogénea (Excel/PDF/texto) se convierte en planilla validada contra el catálogo con matching exacto+barcode, cliente mapeado y ambigüedad señalada — reduciendo el tiempo de decenas de minutos hacia 2 min — **sin reemplazar el criterio humano**.

## 2. Criterios de aceptación del MVP (mínimo para darlo por cumplido)

1. Dada una orden con CUIT/razón social conocidos, el sistema identifica al cliente o marca "cliente no mapeado".
2. Dadas líneas con código exacto o EAN, el sistema matchea al código interno e indica cómo (código exacto / barra).
3. Dada una descripción genérica con múltiples candidatos, el sistema marca "revisar: N candidatos" y **no elige solo**.
4. El operador puede corregir inline y exportar a Excel en 1 clic con log de validaciones.
5. Dada una foto ilegible, el sistema responde "ilegible — pedir reenvío legible".

## 3. Núcleo vs. stretch vs. fuera

- **Núcleo (compromiso):** detección de cliente + matching exacto/barcode + import/export + detección de ambigüedad.
- **Stretch (si alcanza el tiempo):** texto libre (requiere pipeline LLM propio), cantidades por cliente, conversión de unidades, catálogo visible.
- **Fuera:** OCR sobre fotos borrosas.

## 4. Hipótesis que el MVP debe validar

| # | Hipótesis | Cómo se mide |
|---|---|---|
| H1 | El matching exacto+barcode resuelve la mayor frustración (duplicados) | % líneas auto-matcheadas sin intervención |
| H2 | Detectar ambigüedad (sin resolver) es suficiente y confiable | % ambigüedades detectadas vs. falsos negativos |
| H3 | El tiempo por orden baja a menos de 5 min (meta 2) | Medición con usuario operativo |
| H4 | El operador mantiene control y confía (no siente reemplazo) | Test cualitativo post-uso |

## 5. Riesgos del MVP y mitigación

- **Riesgo de alcance:** mitigado con regla de caída (texto libre/ambigüedad → v2).
- **Tabla de conversión de unidades no confirmada:** no bloquea el núcleo.
- **Dependencia de calidad de entrada:** flujo alternativo "pedir reenvío".
- **Pipeline LLM (PDF):** costo/latencia por orden y privacidad a evaluar en spike.

## 6. Trazabilidad

Problema → Evidencia → Funcionalidad (`prioritization`) → Este MVP → User stories → Tests.
