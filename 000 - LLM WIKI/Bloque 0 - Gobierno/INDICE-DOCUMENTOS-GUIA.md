Índice único de todos los documentos de la guía del agente: los que viven en la raíz del repositorio (`CLAUDE.md`, `SPEC.md`) y en su contenedor `000 - LLM WIKI/` (`Bloque 0-2`). No cubre el espacio hermano `100 - PROYECTO ACTIVO/`, que tiene su propio índice. Sirve para ubicarlos todos desde un solo lugar sin tener que recorrer las 3 carpetas de bloques.

**Regla de precedencia entre estos documentos:** `CLAUDE.md` > `SPEC.md` > `BITACORA-DECISIONES.md`. Ver detalle en `CLAUDE.md`.

## Raíz

| Documento                                                                | Rol                                                                                                 |
| :----------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| [[CLAUDE]]                                                               | Fuente de verdad vigente — operación diaria del agente                                              |
| [[SPEC]]                                                                 | Material fundacional/histórico — no se edita en paralelo a `CLAUDE.md`                              |
| [[GEMINI]]                                                              | Puente ligero de compatibilidad multi-agente (redirige a [[CLAUDE]])                               |
| `README.md`                                                              | Portada del repositorio, para lectores humanos — no es documento normativo                          |
| `referencias-externas/llm-wiki.md`                                       | Material fundacional externo, de terceros — el patrón "LLM Wiki" en el que se inspira este proyecto |

## Bloque 0 — Gobierno

| Documento                                  | Rol                                                              |
| :----------------------------------------- | :--------------------------------------------------------------- |
| [[00-VISION]]                              | Visión, principios rectores (11), modelo de entidades            |
| [[BITACORA-DECISIONES]]                    | Historial de decisiones nuevas conforme se toman                 |
| [[CONVENCIONES-ESCRITURA]]                 | Estilo de redacción de toda la bóveda                            |
| [[CHECKLIST-ARRANQUE-PROYECTO-NUEVO]]      | Pasos para instanciar la wiki sobre un proyecto de software nuevo |
| [[reporte-actual]]                         | Salida de los subagentes — estado de la corrida más reciente     |
| [[historico-auditorias]]                   | Salida de los subagentes — log histórico de todas las corridas   |
| [[LEEME-GOBIERNO]]                         | Índice propio del bloque                                         |

## Bloque 1 — Modelo de requerimiento

| Documento                                  | Rol                                                  |
| :----------------------------------------- | :--------------------------------------------------- |
| [[MODELO-REQUERIMIENTO]]                   | Fases, tarea, stopper, derivación del Estado Macro   |
| [[plantilla-requerimiento-cliente]]        | Plantilla normativa                                  |
| [[plantilla-hoja-principal-requerimiento]] | Plantilla normativa                                  |
| [[plantilla-seguimiento-requerimiento]]    | Plantilla normativa (incluye tabla de trazabilidad)  |
| [[plantilla-conclusion-requerimiento]]     | Plantilla normativa                                  |
| [[plantilla-mapeo-excepcion-jerarquia]]    | Plantilla normativa — solo para excepciones formales |
| [[LEEME-MODELO-DE-REQUERIMIENTO]]          | Índice propio del bloque                             |

## Bloque 2 — Ontología y relaciones

| Documento | Rol |
| :--- | :--- |
| [[ONTOLOGIA]] | Modelo normativo completo, cardinalidades, diagrama ER |
| [[ESTANDAR-FRONTMATTER-Y-FECHAS]] | Estándar normativo |
| [[REGLA-IDENTIFICADOR-WS]] | Estándar normativo |
| [[plantilla-contrato-ws]] | Plantilla normativa |
| [[plantilla-historia-de-usuario]] | Plantilla normativa |
| [[plantilla-flujo-funcional]] | Plantilla normativa |
| [[GLOSARIO]] | Glosario de términos |
| `Manual de Diligenciamiento Formato Historia de Usuario v.2` | Fuente de cliente inmutable (P9) |
| [[LEEME-ONTOLOGIA-Y-RELACIONES]] | Índice propio del bloque |

**Regla de uso:** este índice se actualiza solo cuando se agrega, retira o renombra un documento normativo de `Bloque 0-2`, `CLAUDE.md` o `SPEC.md` — no ante cada edición de contenido interno (P11, P4).
