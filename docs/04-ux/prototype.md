# Prototype — Parity (Mensajes + Estructura)

> **Origen:** `Documento de marca.docx:6-8` (Tagline, mensajes principales, mensajes página principal) + `Diseño UX-UI/Logo + nombre final.pdf` + `flujo_estandarizador_para_empleado.svg` (interacción Dashboard). Estado: copy sujeto a cambios (confirmado 2026-09-07), estructura lista para wireframe.

## 1. Tagline / Claim

**Candidatos (4) — `Documento:68-71` `[Frase 1-4]` — propuesta en tono venta universal:**

1. *Orden desordenada entra, pedido validado sale.*
2. *Sin re-tipeo. Sin dudas ocultas.*
3. *Cualquier formato. Un solo clic.*
4. *La tecnología asiste, tú decides.*

**Claim principal elegido (para lockup hero):**
> **Orden desordenada entra, pedido validado sale. Sin re-tipeo, sin dudas ocultas.**
> — Fusión de candidatos 1+2, coherente con Propósito/Visión (`ux-ui-guidelines.md:1`)

**Qué transmite:** Claridad inmediata + promesa de control humano (no "mágico"). Aplica a paridad naming: `parity` (software, acción) + `Parity` (marca-persona, confianza).

## 2. Mensajes principales (`Documento:77-86`)

| Slot | Mensaje | Nota |
|---|---|---|
| **Mensaje principal (recuerdo)** | *Tu pedido, validado y listo en segundos — sin cambiar tu forma de trabajar.* | Para que recuerden beneficio + no-desplazamiento |
| **Problema** | *Cada cliente manda su pedido a su manera: WhatsApp, mail, PDF, foto. Traducirlo a mano quita horas y suma errores.* | Universal, sin citar empresa |
| **Solución** | *parity lee cualquier formato, lo cruza con tu catálogo y te lo deja en una tabla familiar, marcando lo que necesita tu ojo.* | Incluye detección, no adivinanza |
| **Beneficio** | *Horas devueltas, errores evitados, control intacto. Exportas en un clic, con trazabilidad.* | Cuantificable sin números fijos |
| **Diferencial** | *No reemplaza tu criterio. Lo potencia. Señala lo ambiguo, no lo inventa — y aprende de cada corrección.* | vs. OCR/IA que "adivina" |

## 3. Mensajes para la página principal (`Documento:88-100`)

### Hero
- **Título:** *Pedidos sin fricción.*
- **Subtítulo (1-2 líneas):** *Sube la orden como te llegue —WhatsApp, mail, PDF o foto— y obtén una planilla validada contra tu catálogo en segundos. Tú revisas, parity ordena.*
- **CTAs:** `[CTA principal]` **Probar con mi catálogo** (primario `#03F07C`) · `[CTA secundario]` **Ver flujo en 30s** (ghost)

### Sección Problema (`Documento:93-94`)
- **Título:** *Tu día no debería ser re-tipeo.*
- **Texto:** *Formatos distintos, códigos que no coinciden, descripciones ambiguas, unidades que cambian por cliente. Lo que debería ser cargar un pedido termina siendo traducir, corregir y volver a pedir.*

### Sección Solución (`Documento:96-97`)
- **Título:** *De caos a planilla en segundos.*
- **Texto:** *parity extrae productos y cantidades, matchea por código o barra, mapea cliente y te muestra una grilla tipo Excel. Lo dudoso queda marcado para que decidas. Exportas en un clic, listo para tu sistema.*

### Sección Confianza (`Documento:99-100`)
- **Título:** *Confianza a la vista. Control en tus manos.*
- **Texto:** *Validación trazable: cada fila dice cómo se matcheó (código exacto / barra / manual). Sin caja negra. Sin sorpresas en facturación. Con log para auditoría.*

## 4. Estructura de prototipo (wireframe sugerido)

**Página principal:** Hero (logo dual `Logo parity sin fondo` según modo, claim, CTAs) → Problema (3 cards: formato/unidad/código) → Solución (diagrama flujo 8 nodos `flujo.svg`) → Confianza (badges verde/ámbar/rojo) → Prueba (uploader) → Footer.

**Dashboard (pantalla core):**
- Top: uploader (drag&drop + “Canal conectado entra automático / Carga manual arrastrar” — labels del SVG) + selector cliente mapeado
- Centro: grilla Excel (`Código | Código Proveedor | Descripción | Proveedor | Unidades | Display | U.Compra | Costo U. | Total | Estado`) — celdas editables, badges `ok (#03F07C) / revisar (#D5A129/#FFF9EC) / error`
- Bottom: `¿Todo correcto?` → `[Corregir la orden: edición tipo Excel]` vs `[Exportar a Excel: un clic, listo para enviar]` (labels exactos del SVG, colores `design-system.md`)

**Estados a prototipar:**
- Happy path (todo ok → export), con cliente mapeado por barra
- Con dudas (ambiguo “alfajor guaymallén 3 candidatos”, unidad dudosa, precio desactualizado)
- Con foto ilegible (PP4b) → mensaje “ilegible — pedir reenvío legible” (fuera MVP)
- Light (`#FFF9EC` bg, letras negras logo) / Dark (`#000000` bg, letras blancas logo)

## 5. Banco creativo / Frases inspiración (`Documento:150-161`)

*Sobre el producto:*
- “Claridad operativa, no magia.”
- “Un clic, no una traducción.”

*Sobre el problema:*
- “Tu cliente no va a cambiar su formato. Tú no deberías tener que traducirlo.”

*Sobre la solución:*
- “De mensaje disperso a planilla perfecta.”

*Sobre filosofía:*
- “Estandarizar es respetar el tiempo de quien vende.”

*Sobre tecnología + personas:*
- “Automatizamos lo repetitivo. Respetamos tu criterio.”
- “La tecnología asiste, tú decides.” (`Documento:145`)

> Todas sujetas a cambios — son el banco para web, slides y comunicación.

## 6. Próximos pasos de prototipo

- [ ] Wireframe Figma (hero + dashboard) con paleta `#03F07C/#5DE9AA/#FFF9EC` y tipografía a elegir de las 11 opciones (`design-system.md:3`)
- [ ] Prototipo clicable del flujo `user-flows.md` (8 nodos) con datos reales `lista_articulos.xlsx` (2.119 SKUs) + `OC_N_94325` (ejemplo validado)
- [ ] Test con usuario tipo Juan (supervisor) — validar que edición tipo Excel no desplaza del sistema habitual

---
*Referencias: `Documento:6-8` `[Frase]` placeholders completados en tono venta; dirección visual sigue “en investigación” (`ux-ui-guidelines.md:4`).*
