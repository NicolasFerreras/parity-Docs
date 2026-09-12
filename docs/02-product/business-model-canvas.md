---
title: "Business Model Canvas"
---

# Business Model Canvas — Parity

> Documento público. Modelo de negocio en 9 bloques.

## 1. Segmentos de cliente

| Segmento | Detalle |
|---|---|
| **Usuarios directos** | Empleados administrativos, de facturación, logística y ventas que reciben, verifican y cargan órdenes. |
| **Comprador** | La distribuidora como organización (licencia). Hipótesis a validar comercialmente. |
| **Usuarios indirectos** | Los clientes que generan las órdenes (no usan Parity, pero determinan los formatos). |

## 2. Propuesta de valor

**Orden desordenada entra, pedido validado sale. Sin re-tipeo, sin dudas ocultas, con control humano hasta el final.**

- Convierte pedidos heterogéneos (WhatsApp, mail, PDF, Excel, foto) en planilla validada contra catálogo en segundos.
- No reemplaza al empleado — lo asiste: señala lo ambiguo, no lo adivina.
- Detalle: `value-proposition.md`.

## 3. Canales

- **Entrada:** WhatsApp, email, PDF, Excel, texto plano, foto — solo carga manual en MVP.
- **Entrega:** dashboard tipo Excel + exportación 1-clic al formato del sistema interno.
- **Comercial (hipótesis):** venta directa a distribuidoras.

## 4. Relación con clientes

- **Asistencia, no reemplazo:** la última palabra es del usuario.
- **Trazabilidad visible:** cada fila dice cómo se matcheó (código exacto / barra / manual) — genera confianza.
- **Aprendizaje por uso:** las correcciones alimentan equivalencias por cliente (v2).

## 5. Fuentes de ingreso (a definir)

- Hipótesis a evaluar: licencia por empresa (SaaS) y/o por volumen de órdenes procesadas.
- Sin modelo de pricing hasta validar con decisores.

## 6. Recursos clave

- Catálogo interno (miles de SKUs, múltiples columnas de código de barras).
- Tabla de mapeo cliente (razón social / CUIT / sucursal → código interno) — prerrequisito.
- Motor de matching (código exacto → barcode → detección de ambigüedad).
- Parser e importador/exportador de documentos.

## 7. Actividades clave

1. Extraer productos y cantidades de cualquier formato de entrada.
2. Matchear contra catálogo y mapear cliente.
3. Señalar ambigüedad y duplicados para revisión humana.
4. Exportar al formato interno + log de validaciones (auditoría).

## 8. Socios clave

- Distribuidoras validadoras del dominio y datos reales.
- Equipo de producto + docentes (criterio impacto + frecuencia + riesgo + viabilidad).

## 9. Estructura de costos (a definir)

- Costo mayor conocido: construir el pipeline de interpretación de texto por primera vez (prompts, errores del modelo, costo/latencia por orden, testing no determinístico).
- Infra mínima: servicios gestionados de base, storage y hosting.
