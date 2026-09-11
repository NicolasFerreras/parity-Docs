---
title: "Estado del proyecto"
description: "Qué existe hoy, qué está en progreso y próximas prioridades de Parity."
---

# Estado del proyecto

Parity está en fase fundacional de MVP. La plataforma ya cuenta con la arquitectura base, la infraestructura y varios módulos de negocio, pero el flujo completo de punta a punta aún se está consolidando.

## Etapa actual

El proyecto superó la etapa de prototipo. Ya dispone de repositorios separados, persistencia en base de datos, documentación y especificaciones de API.

El objetivo ahora es conectar los flujos de producto de extremo a extremo:

<CardGroup cols={2}>
  <Card title="Ciclo de importación" icon="file-spreadsheet">
    El usuario sube un Excel o PDF, la plataforma extrae y valida líneas y genera una vista previa.
  </Card>
  <Card title="Ciclo de matching" icon="git-compare">
    La plataforma cruza cada línea contra el catálogo por código o barra y marca exactos, ambiguos y fallidos.
  </Card>
  <Card title="Ciclo de revisión" icon="table">
    El usuario revisa en tabla, corrige fallidos y exporta en un clic al formato interno.
  </Card>
  <Card title="Ciclo de observación" icon="activity">
    Logs estructurados y validación permiten auditar qué se importó y cómo se resolvió.
  </Card>
</CardGroup>

## Qué existe hoy

| Área | Estado | Significado operativo |
| --- | --- | --- |
| Documentación | Activa en Mintlify | Producto, técnico y operaciones centralizados. |
| API | Go + PostgreSQL en Docker | Orquesta validación, matching y persistencia. |
| Interfaz | React + TypeScript | Subida, revisión y edición manual. |
| Catálogo | PostgreSQL | Fuente durable de productos y códigos. |
| Infraestructura | Docker Compose | Stack reproducible local y productivo. |

## Próximas prioridades

1. Validar de extremo a extremo la importación de Excel y el matching por código/barra.
2. Endurecer el contrato de API antes de que el frontend dependa fuertemente de él.
3. Completar la integración de la interfaz con la API con estados de carga y error consistentes.
4. Sincronizar la especificación OpenAPI en el repositorio de docs.
5. Definir el flujo de documentación bilingüe antes de traducir cada página.
