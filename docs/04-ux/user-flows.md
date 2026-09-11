# User Flows — Parity

> **Origen:** `Relevamiento y Descubrimiento/flujo_estandarizador_para_empleado.svg` (680×780, 8 nodos, 7 transiciones) + `01-research/user-journey.md` (5 etapas AS-IS) + `Documento de marca` principios. Todos los flujos mantienen el principio “La tecnología asiste, la persona decide”.

## 1. Flujo principal — Estandarizar orden para el empleado (happy path)

**Diagrama fuente:** `flujo_estandarizador_para_empleado.svg` / `.png` — Título: “Flujo de la plataforma para el empleado” — Desc: “Cómo una orden entra al sistema, es procesada, revisada en dashboard y exportada a Excel o corregida si tiene errores.”

```
[Orden de compra: WhatsApp, email, PDF, foto]
        ├─► [Canal conectado: entra automático]
        └─► [Carga manual: arrastrar, copiar, pegar]
                        │
                        ▼
          [Sistema extrae info: identifica productos y cantidad]
                        │
                        ▼
          [Dashboard: el empleado revisa la orden]
                        │
                        ▼
               ◇ ¿Todo correcto? ◇
                 /            \
              No (→)        Sí (→)
               /                \
[Corregir la orden: edición  [Exportar a Excel: un clic,
 tipo Excel]  ── vuelve a     listo para enviar]
 revisión
```

**Pasos detallados (con correspondencia `01-research/user-journey.md`):**

| # | Nodo SVG | Acción usuario | Sistema | Salida |
|---|---|---|---|---|
| 1 | Orden de compra | — | — | Input heterogéneo (cualquier canal) |
| 2a | Canal conectado | — | Webhook/mail listener ingesta automática | Orden en cola, con metadata cliente (CUIT/razón social) |
| 2b | Carga manual | Drag&drop / copy-paste / upload | — | Alternativa cuando no hay canal conectado (MVP incluye ambas) |
| 3 | Sistema extrae | — | Parser + matching: 1) código exacto `codigo` 2) barcode `codbarra/2/3` (2.119 SKUs `lista_articulos.xlsx`) 3) mapeo cliente CUIT→código 4) detección ambigüedad (marca, no resuelve) | Grilla precargada con estados ok/revisar/error |
| 4 | Dashboard | Revisa grilla tipo Excel (ver `design-system.md` columnas `Código|Código Proveedor|Descripción|Unidades|Display|U.Compra`) | Resalta dudas ámbar `#D5A129`, ok verde `#03F07C` | Decisión |
| 5 | ¿Todo correcto? | Sí → Exportar / No → Corregir | — | — |
| 6a | Exportar a Excel | 1 clic | Genera `OC_*.xlsx` formato interno + log de validaciones | Listo para enviar/facturar |
| 6b | Corregir | Edita celdas inline, elige alternativa sugerida | Revalida | Vuelve a 4 |

## 2. Flujos alternos / edge

| Caso | Flujo | Estado actual MVP |
|---|---|---|
| **Foto borrosa (PP4b)** | Entrada → Extrae falla OCR → Dashboard marca “ilegible — pedir reenvío legible” → salida manual | **Fuera de MVP** por viabilidad 1/5 (`pain_points_a_mvp.md:67` + entrevista Juan “quedan borrosos los números”). No se invierte en OCR en v1; se mantiene proceso actual “pedir reenvío”. |
| **Código cliente no viene (PP5)** | Extrae CUIT/razón social → busca en tabla mapeo → si no existe → badge ámbar “cliente no mapeado” → empleado selecciona código de lista | **Dentro MVP** (prerrequisito, score 19). Sin esto no se puede exportar. |
| **Duplicado por packaging (PP2)** | Cliente manda código viejo → sistema busca EAN en 3 columnas → encuentra `codigo` vigente → badge verde “match por barra” + tooltip “código viejo → nuevo” | **Dentro MVP** (core, score 18, mayor frustración) |
| **Unidad no coincide (PP3) / Cantidad multi-formato (PP6)** | Sistema importa `Unidades/Display/U.Compra` tal cual → si equivalencia conocida, sugiere conversión; si no, deja tal cual + nota | **Fuera MVP / v2** (PP3 viabilidad 3, PP6 3) — se resuelve caso por caso por cliente |
| **Descripción ambigua (PP1)** | Descripción genérica (“alfajor guaymallén”) → match múltiple → estado “revisar: 3 candidatos” → empleado elige | **Dentro MVP como detección, no resolución automática** (viabilidad 2) |
| **Precios/condiciones desactualizadas** | Compara `Costo U.` vs. maestro promociones → alerta | v2 (requiere maestro promociones) |

## 3. Estados de la grilla (para `design-system.md` y `prototype.md`)

- **ok** (verde `#03F07C`) — match exacto o por barra único
- **revisar** (ámbar `#D5A129`, fondo `#FFF9EC`) — duplicado, ambiguo, cliente no mapeado, unidad dudosa — editable
- **error** (rojo `color-error`) — código inexistente, cantidad vacía, EAN no encontrado
- **vacío** — gris deshabilitado

## 4. Reglas de negocio transversales

- **Nunca auto-facturar:** exportar es explícito, no automático.
- **Trazabilidad:** cada fila exportada guarda log “match por: código exacto | barra | manual” para auditoría futura (`user-journey.md: oportunidad “Registrar reglas de validación”`).
- **Aprendizaje v2:** las correcciones manuales alimentan tabla de equivalencias por cliente (PP6).

## 5. Referencias

- **AS-IS 5 etapas:** Lectura → Revisión razón social → Validación precios → Control productos → Carga (`01-research/user-journey.md:30`)
- **TO-BE 6 pasos:** este flujo colapsa las 5 etapas manuales en recepción → extracción/matcheo → revisión → confirmación → exportación.
- **Assets:** `flujo_estandarizador_para_empleado.svg` (código SVG inspeccionado, 7 líneas/poly) + `.png` (440KB) en `Entregables facu/Relevamiento...`

---
*Próximo: wireframes de Dashboard (grilla, badges, edición inline, export) en `prototype.md`.*
