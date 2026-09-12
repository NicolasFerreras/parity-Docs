---
title: "Flujo del usuario"
---

# User Flows — Parity

> Flujo de la plataforma para el empleado (8 nodos): cómo una orden entra al sistema, es procesada, revisada en dashboard y exportada o corregida. Todos los flujos mantienen el principio “La tecnología asiste, la persona decide”.

## 1. Flujo principal — Estandarizar orden para el empleado (happy path)

```mermaid actions={true}
flowchart TD
    A[Usuario arrastra Excel o PDF a la zona de carga] --> B[Plataforma extrae líneas, valida estructura y cantidades]
    B --> C[Sistema cruza cada línea contra el catálogo por código o barra]
    C --> D[Tabla muestra resultados con estados y permite editar fallidos]
    D --> E[Usuario confirma y exporta en un clic]
```

Detalle del flujo completo (8 nodos):

```mermaid actions={true}
flowchart TD
    A[Orden de compra: WhatsApp, email, PDF, foto] --> C[Carga manual: arrastrar, copiar, pegar]
    C --> D[Sistema extrae info: productos y cantidad]
    D --> E[Dashboard: el empleado revisa la orden]
    E --> F{¿Todo correcto?}
    F -->|Sí| G[Exportar a Excel: un clic, listo para enviar]
    F -->|No| H[Corregir la orden: edición tipo Excel]
    H --> E
```

**Pasos detallados:**

| # | Nodo | Acción usuario | Sistema | Salida |
|---|---|---|---|---|
| 1 | Orden de compra | — | — | Input heterogéneo (cualquier canal) |
| 2 | Carga manual | Drag&drop / copy-paste / upload | — | Única vía de entrada en MVP (sin bot ni ingesta automática) |
| 3 | Sistema extrae | — | Parser + matching: código exacto, barcode (3 columnas EAN), mapeo cliente, detección ambigüedad (marca, no resuelve) | Grilla precargada con 4 estados |
| 4 | Dashboard | Revisa grilla tipo Excel | Resalta dudas ámbar, ok verde | Decisión |
| 5 | ¿Todo correcto? | Sí → Exportar / No → Corregir | — | — |
| 6a | Exportar a Excel | 1 clic | Genera formato interno + log de validaciones | Listo para enviar/facturar |
| 6b | Corregir | Edita celdas inline, elige alternativa sugerida | Revalida | Vuelve a 4 |

## 2. Flujos alternos / edge

| Caso | Flujo | Estado actual MVP |
|---|---|---|
| **Foto borrosa** | Entrada → Extrae falla OCR → Dashboard marca “ilegible — pedir reenvío legible” → salida manual | **Fuera de MVP** por viabilidad baja. No se invierte en OCR en v1; se mantiene proceso actual “pedir reenvío”. |
| **Código cliente no viene** | Extrae CUIT/razón social → busca en tabla mapeo → si no existe → badge ámbar “cliente no mapeado” → empleado selecciona código de lista | **Dentro MVP** (prerrequisito). Sin esto no se puede exportar. |
| **Duplicado por packaging** | Cliente manda código viejo → sistema busca EAN en 3 columnas → encuentra código vigente → badge verde “match por barra” + tooltip “código viejo → nuevo” | **Dentro MVP** (núcleo, mayor frustración operativa) |
| **Unidad no coincide / Cantidad multi-formato** | Sistema importa `Unidades/Display/U.Compra` tal cual → si equivalencia conocida, sugiere conversión; si no, deja tal cual + nota | **Fuera MVP / v2** — se resuelve caso por caso por cliente |
| **Descripción ambigua** | Descripción genérica (“alfajor guaymallén”) → match múltiple → estado “revisar: 3 candidatos” → empleado elige | **Dentro MVP como detección, no resolución automática** |
| **Precios/condiciones desactualizadas** | Compara `Costo U.` vs. maestro promociones → alerta | v2 (requiere maestro promociones) |

## 3. Estados de la grilla (para `design-system.md` y `prototype.md`)

- **ok** (verde `#03F07C`) — extraído idéntico a catálogo, sin tocar nada
- **revisar** (ámbar `#D5A129`, fondo `#FFF9EC`) — requiere cualquier retoque o es de origen LLM — editable
- **error** (rojo `color-error`) — dato presente pero inválido (código inexistente, cantidad vacía, EAN no encontrado)
- **faltante** (gris) — dato ausente en origen

## 4. Reglas de negocio transversales

- **Nunca auto-facturar:** exportar es explícito, no automático.
- **Trazabilidad:** cada fila exportada guarda log “match por: código exacto | barra | manual” para auditoría futura.


## 6. Recorrido del usuario (AS-IS)

```mermaid
journey
    title Cargar pedido (AS-IS)
    section 1 Lectura de orden
      Decodifica orden multicanal: 2: Usuario operativo
    section 2 Revisión de cliente
      Contrasta datos fiscales: 2: Usuario operativo
    section 3 Validación de precios
      Compara importes y promos: 2: Usuario operativo
    section 4 Control de productos
      Traduce códigos y descripciones: 1: Usuario operativo
    section 5 Carga para facturación
      Tipeo manual: 1: Usuario operativo
      Pedido terminado: 4: Usuario operativo
```

## 7. Referencias

- **AS-IS 5 etapas:** Lectura → Revisión de cliente → Validación precios → Control productos → Carga
- **TO-BE:** este flujo colapsa las 5 etapas manuales en recepción → extracción/matcheo → revisión → confirmación → exportación.
- **Correspondencia con alcance** (`02-product/scope.md`): flujo principal = mapeo cliente + matching + import/export + detección ambigüedad; foto borrosa fuera; unidad/cantidad y texto libre en stretch.

---
*Próximo: wireframes de Dashboard (grilla, badges, edición inline, export) en `prototype.md`.*
