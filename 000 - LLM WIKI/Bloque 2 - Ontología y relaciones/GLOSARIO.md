---
id_documento: GLOSARIO-B2
tipo_documento: norma-contenido
bloque: Bloque 2 - Ontología y relaciones
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P9
  - P10
  - P11
fecha_creacion: 2026-07-27
fecha_actualizacion: 2026-10-18
estado: Aprobado
---

# Glosario del Proyecto

Glosario único de la wiki. Unifica los términos del dominio funcional (heredados de [[Manual de Diligenciamiento Formato Historia de Usuario v.2]], fuente de cliente) con las 7 entidades de primer nivel de [[ONTOLOGIA]]. No repite la definición formal de cada entidad — remite a la ontología cuando aplica (P4).

---

## Términos vigentes en este modelo

| Término | Definición | Dónde vive |
| :--- | :--- | :--- |
| **Historia de Usuario (HU)** | Unidad de valor funcional para un actor, dentro de un paso de flujo. Formato "Como [rol], quiero [objetivo], para [beneficio]". | `plantilla-historia-de-usuario.md` |
| **Regla de Negocio (RN)** | Restricción o política de negocio obligatoria, indivisible, con identidad propia (`RN-01`, `RN-02`...). | Ficha dentro de HU o WS |
| **Web Service (WS)** | Contrato técnico de integración (request/response/SLA), una ficha por endpoint. | `plantilla-contrato-ws.md` |
| **Criterio de Aceptación** | Condición verificable, en formato Gherkin (Dado/Cuando/Entonces), que define cuándo una HU está completa. | Sección 4 de la HU |
| **Product Owner (PO)** | Responsable del negocio y de maximizar el valor del producto. Único escritor junto al agente (P3). | Rol, no documento |
| **Mockup / Prototipo** | Representación visual de interfaz, orientativa y no contractual. | Sección 5 de la HU |
| **Backlog** | Lista priorizada de requerimientos y tareas pendientes. En esta wiki, vive como tabla del documento de Seguimiento, no como página propia. | `plantilla-seguimiento-requerimiento.md` |
| **Pre-condiciones** | Requisitos o estados que deben cumplirse antes de ejecutar una HU. | Sección 1 de la HU |
| **Actor** | Rol de usuario que ejecuta la acción (ej. Empleado registrado). No es genérico ("usuario"). | Campo en HU y Flujo |
| **Flujo** | Vertiente o mapa de navegación de una funcionalidad, documentado con diagrama Mermaid. | `plantilla-flujo-funcional.md` |
| **Paso de Flujo** | Unidad de interacción del usuario dentro de un flujo (`P-01`, `P-02`...). | Ficha dentro del Flujo |
| **Stopper** | Bloqueante rastreable con responsable externo y antigüedad. | Fila en Seguimiento |
| **Tarea** | Unidad de registro de toda actividad del requerimiento, con fase, estado y horas. | Fila en Seguimiento |
| **Requerimiento** | Unidad funcional principal del producto, identificada por sigla y correlativo. | Carpeta propia |
| **Estado Macro** | Estado derivado (nunca escrito a mano) del requerimiento: `Sin iniciar` · `En curso` · `Bloqueado` · `Cerrado en Producción (Dormido)`. | `MODELO-REQUERIMIENTO.md` §1.3 |

---

## Términos del manual de cliente que NO existen como entidad propia en este modelo

Se documentan aquí para que el agente entienda por qué, si alguien los menciona, no debe crear un campo ni documento nuevo para ellos.

| Término del manual              | Por qué no aplica igual aquí                                                                                                                          |
| :------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Épica / Feature**             | Se conserva como campo descriptivo dentro de la Identificación de la HU (contexto de agrupación), nunca como documento o entidad independiente (P11). |
| **Sprint**                      | Campo opcional de la **Tarea** (`SPR-NN`), no de la HU (DEC-11). Registrarlo en la HU duplicaría el dato.                                             |
| **Puntos de Historia**          | No se usa. El esfuerzo de esta wiki se mide en horas estimadas/consumidas de la Tarea (P7), no en puntos relativos.                                   |
| **Estado (de la HU)**           | No se usa a nivel de HU. El estado y el avance ya se rastrean en la Tarea correspondiente del documento de Seguimiento                                |
| **Refinamiento (Grooming)**     | Es una actividad, no una entidad. Se registra como Tarea en la fase `1. REQUERIMIENTO` o `2. DISEÑO` si el PO decide dejarla trazada.                 |
| **Id. Herramienta de Proyecto** | No aplica (P2 — cero dependencias externas, sin Jira/Azure DevOps).                                                                                   |
