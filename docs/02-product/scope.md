---
title: "Alcance"
---

# Alcance (Scope) — Parity

> Documento público. Qué entra al MVP, qué es stretch y qué está explícitamente fuera, con trazabilidad a dolores.

## 1. Dentro del MVP (núcleo comprometido)

| Funcionalidad | Dolor que ataca | Base |
|---|---|---|
| Detección de código de cliente (tabla razón social/CUIT → código) | Sin esto no se carga ningún pedido (prerrequisito) | Tabla de búsqueda simple |
| Matching por código exacto + código de barras | Duplicados: mayor frustración operativa | Confirmado con datos reales |
| Importación y exportación de documentos (Excel estructurado validado) | Transversal | Parse/export + storage centralizado |
| Detección (no resolución) de ambigüedad en descripción | Ambigüedad: síntoma más frecuente | Reglas determinísticas (texto aproximado + trigramas); LLM solo como ayuda opcional |

## 2. Stretch del MVP (condicional — decisión de riesgo del equipo)

Se intenta todo lo de abajo en el MVP, dejando fuera solo OCR. Si el tiempo no alcanza, **texto libre y/o detección de ambigüedad caen a v2 sin comprometer el resto**.

| Funcionalidad | Condición |
|---|---|
| Interpretación de pedidos en texto libre (cuerpo mail/WhatsApp) | Requiere pipeline LLM propio |
| Traducción de "cantidad" según formato del cliente (cajas/unidades/display/bulto) | Caso por caso por cliente |
| Conversión automática de unidades (sueltas vs. docena) | Solo si se confirma tabla de conversión |
| Visualización de catálogo de productos y clientes | Panel de consulta rápida |

**Fundamento:** la grilla de priorización evalúa cada funcionalidad por valor (evidencia de research) vs. esfuerzo (estimación técnica). El costo alto de un pipeline LLM está en construirlo la primera vez (prompts, errores del modelo, costo/latencia por orden, testing no determinístico).

## 3. Explícitamente fuera del MVP

| Funcionalidad | Motivo |
|---|---|
| OCR sobre fotos borrosas de WhatsApp | Viabilidad baja; existe solución no-técnica (pedir reenvío legible) |

## 4. Trazabilidad dolor → funcionalidad

- **Código cliente ausente → detección de cliente** (ninguna orden real trae el código esperado).
- **Duplicados → matching por barcode** (resuelve cambio de packaging).
- **Ambigüedad → detección** (marca, no adivina).
- **Cantidad por cliente → traducción de cantidad** (v2 caso por caso).
- **Conversión de unidades → conversión automática** (requiere tabla no confirmada).
- **Texto libre → interpretación** (stretch); **foto borrosa → fuera**.
