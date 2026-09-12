---
title: "UX/UI Guidelines"
---

# UX/UI Guidelines — Parity

> Guía de tono, identidad y principios de Parity. Referencia para todo `04-ux`.

## 1. Identidad general

| Campo | Definición final (venta universal, sin citar caso) |
|---|---|
| **Nombre** | **Parity** (producto como persona) / **parity** (software, ej. “subir archivo a parity”) / **PARITY** (variante mayúsculas) — preservar distinción. Uso: *“Parity es simpleza, calidad y precisión”* vs *“subir archivo a parity”* |
| **Descripción breve** | Plataforma que convierte pedidos desordenados —WhatsApp, mail, PDF, Excel o foto— en datos validados y listos para exportar en un clic, sin re-tipeo. |
| **Propuesta de valor** | Orden desordenada entra, pedido validado sale. Sin re-tipeo, sin dudas ocultas, con control humano hasta el final. Ahorra horas, reduce errores, mantiene tu criterio. |
| **Propósito** | **Parity existe para convertir el caos de pedidos en claridad operativa y devolverle horas a quien hace que el negocio avance. Orden desordenada entra, pedido validado sale. Sin re-tipeo, sin dudas ocultas.** |
| **Visión** | **Ser el estándar invisible detrás de cada venta. Pedidos que se entienden solos, se cargan solos, fluyen solos — con cualquier cliente, en cualquier formato, en cualquier empresa que venda productos.** |
| **Misión** | **Hoy transformamos mensajes, planillas y PDFs dispersos en una sola vista clara, validada y exportable. Automatizamos lo repetitivo, asistimos lo crítico y respetamos tu criterio hasta el final.** |

## 2. Esencia de marca

**Conceptos que queremos transmitir:**
Simplicidad · Confianza · Precisión · Eficiencia · Transparencia · Control · Tecnología al servicio de las personas · Orden · Fluidez · Automatización · Validación · Claridad

**Valores (4):**
1. **Precisión** — Cada código se reconoce, cada producto se encuentra. No adivinamos, señalamos.
2. **Control** — La persona decide. La tecnología asiste. La última palabra es del usuario.
3. **Fluidez** — De pedido caótico a planilla lista en segundos, sin cambiar de herramienta.
4. **Confianza** — Validación visible, trazable y exportable en un clic.

## 3. Personalidad

**Si Parity fuera una persona, sería:**
Profesional · Precisa · Confiable · Simple · Moderna · Directa

**NO queremos que se perciba como:**
Compleja · Fría · Reemplazante · Artificial · Burocrática

> Test: ¿Suena a colega eficiente que te saca trabajo de encima, no a robot que te reemplaza?

## 4. Tono de comunicación

**Cómo hablamos:**
Claro · Directo · Profesional · Simple · Cercano

**Cómo NO hablamos:**
Excesivamente técnico · Corporativo · Confuso · Exageradamente informal

**Ejemplos:**
- ❌ “Nuestra solución de ETL con parsers heurísticos normaliza ontologías heterogéneas de SKUs”
- ✅ “Sube el pedido como te llegue. parity lo ordena y tú lo validas en segundos.”
- ❌ “Automatización disruptiva end-to-end que reemplaza tu gestión”
- ✅ “Automatizamos lo repetitivo. Tú mantienes el control.”

## 5. Palabras asociadas

**Usar:** Precisión · Orden · Fluidez · Confianza · Claridad · Eficiencia · Control · Automatización · Validación · Simplicidad

**Evitar:** Reemplazo · Automágico · Complejo · Burocrático · “IA que decide por ti” — transmiten pérdida de control.

## 6. Principios del producto (guían diseño y dev)

1. **La tecnología asiste, la persona decide.** Automatizar lo repetitivo, señalar lo ambiguo, nunca adivinar.
2. **Señalar, no ocultar.** Todo match dudoso se marca (amarillo/rojo), con alternativa visible y campo editable.
3. **No desplazar del sistema habitual.** Grilla tipo Excel, exportación 1-clic al formato interno — no obligar a cambiar de ERP/flujo.
4. **Estandarizar antes de sofisticar.** Primero formato único validado; luego reglas por cliente (unidades, packs) en v2.

## 7. Criterio para futuras decisiones

Ante cada decisión de diseño/comunicación/producto, preguntar:
- ¿Esto representa quiénes somos? (precisión, control, cercanía)
- ¿Simplifica la experiencia o agrega complejidad?
- ¿Transmite confianza y control?
- ¿Ayuda al usuario o solo suena “innovador”?

## 8. Naming convention (regla operativa)

| Contexto | Forma | Ejemplo |
|---|---|---|
| Código, docs técnicos, CTAs de carga | `parity` minúsculas | “Arrastrar archivo a parity”, `api.parity.*` |
| Comunicación de marca, hero, pitch | `Parity` Capitalizada | “Parity es claridad operativa” |
| Logotipo / claim lockup | `PARITY` mayúsculas si el lockup lo exige | `PARITY — Orden entra, pedido sale` |

---
*Referencia visual y copy detallado: `design-system.md` (paleta/tipografía/logos) + `user-flows.md` (flujo 8 nodos + recorrido de usuario).*
