---
title: "Documentación de Parity"
description: "Documentación operativa y de producto para Parity y su infraestructura."
---

# Documentación de Parity

Parity es un producto para estandarizar, formatear y validar órdenes de compra con la menor fricción posible. El sistema combina una plataforma de procesamiento, un catálogo de productos y una interfaz de revisión que convierte pedidos desordenados —Excel, PDF o texto— en datos listos para importar.

Esta documentación está escrita para producto, operaciones e ingeniería. Explica qué busca resolver Parity, cómo funcionan los flujos principales y cómo la arquitectura técnica sostiene esos flujos.

## Qué hace Parity

Parity ayuda a equipos de ventas y administración a:

* Importar órdenes sin reescribir — desde Excel, PDF o texto copiado.
* Validar estructura, cantidades y códigos contra el catálogo.
* Resolver matching exacto por código o barra, y señalar lo ambiguo para revisión humana.
* Revisar en una tabla familiar, editar lo fallido y exportar en un clic al formato interno.

## Componentes principales

| Componente | Propósito |
| --- | --- |
| Plataforma de procesamiento | Orquesta validación, matching y persistencia de órdenes. |
| Catálogo | Fuente de verdad de productos, códigos y barras. |
| Interfaz de revisión | Cliente web para subir, revisar y corregir órdenes. |
| API | Contratos HTTP para ingesta y consulta. |
| PostgreSQL | Fuente durable de órdenes y catálogo. |
| Docker | Empaquetado y ejecución consistente entre entornos. |
| Mintlify | Hosting y renderizado de documentación. |

## Mapa de documentación

* **Resumen** explica lógica de producto, estado actual y glosario.
* **Producto** explica alcance, propuesta de valor, MVP y flujos de usuario.
* **Diseño** explica guías, flujos y sistema de diseño de la interfaz.
* **Técnico** explica arquitectura, decisiones y APIs.

## Etapa actual

Parity está en fase fundacional de MVP. La arquitectura es intencionalmente simple: una API en Go, un frontend en React y una base PostgreSQL, todo orquestado con Docker. El objetivo es validar el flujo completo —de Excel desordenado a pedido validado en segundos— antes de introducir procesamiento asíncrono o infraestructura más pesada.
