---
id_documento: SPEC-PROYECTO
tipo_documento: especificacion-funcional
bloque: Transversal — consolida Bloques 0, 1 y 2
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-27
estado: Aprobado
fuente: Consolida 00-VISION.md, MODELO-REQUERIMIENTO.md, ONTOLOGIA.md
---

# SPEC — LLM Wiki para Gestión de Proyectos de Software

Este documento es el **QUÉ** del sistema: comportamiento esperado y criterios de aceptación. El **CÓMO** (modelo de datos detallado, esquemas YAML completos, reglas técnicas) vive en los documentos normativos ya aprobados ([[ONTOLOGIA]], [[MODELO-REQUERIMIENTO]], [[ESTANDAR-FRONTMATTER-Y-FECHAS]], [[REGLA-IDENTIFICADOR-WS]]). Este spec los referencia; no los repite (P4, P11).

**Para quien implemente esto (Claude Code u otro agente):** los documentos de la carpeta con `estado: Aprobado` en su frontmatter son la fuente de verdad y no deben regenerarse ni reinterpretarse. Este documento es **material fundacional/histórico** para entender el proyecto —  no se edita como instrucción operativa viva; esa instrucción vive únicamente en [[CLAUDE]]. [[CLAUDE]] es la fuente de verdad vigente sobre cómo debe operar el agente; si algo aquí contradice a [[CLAUDE]], gana [[CLAUDE]]. [[BITACORA-DECISIONES]] registra el historial de decisiones nuevas como registro de referencia, sin precedencia sobre ninguno de los dos.

---

## 1. El producto en una frase

Un LLM Wiki con agente y skill que permite llevar un proyecto de software con claridad total de tareas, sin perder nunca la actualización de una definición en todos los documentos relacionados.

**Señal única de éxito:** escribirle al agente y recibir todas las tareas pendientes del día, al día, sin reconstruir nada a mano.

**Criterio de rechazo (anti-objetivo):** cualquier entregable que aumente el número de documentos, filas o estructuras sin aumentar la trazabilidad navegable se descarta de inmediato.

---

## 2. Alcance — 5 funcionalidades núcleo

Cada una de estas 5 preguntas debe poder responderse de forma confiable. Los criterios de aceptación (formato dado/cuando/entonces) están en la sección 8.

|   #   | Funcionalidad                           | Responde a                                                                                                 |
| :---: | :-------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| **1** | **Reporte de pendientes del día**       | ¿Qué tenemos pendiente hoy? ¿Qué nos hace falta?                                                           |
| **2** | **Cálculo de avance por requerimiento** | ¿Qué porcentaje de avance tiene el requerimiento X? (horas ejecutadas / estimadas, con fecha de corte)     |
| **3** | **Resumen semanal**                     | ¿Cuáles fueron los principales avances de la última semana?                                                |
| **4** | **Detección de contradicciones**        | ¿Qué contradicciones existen dentro de un requerimiento o entre requerimientos?                            |
| **5** | **Auditoría de rol**                    | Actuar como un usuario, recorrer el flujo documentado y decir qué paso o servicio no está bien documentado |

---

## 3. Fuera de alcance (No-Goals)

- **No** es un reemplazo del Excel de bolsa de horas ni del cobro al cliente — el Excel conserva el detalle contable (P7).
- **No** es un dashboard visual.
- **No** es un gestor de proyectos multiusuario ni soporta edición concurrente (P3 — un solo escritor: PO + agente).
- **No** es un sistema de investigación abierta (sin scraping, sin agentes paralelos).
- **No** es un analista de negocio: ejecuta, mantiene y señala hechos estructurales; no opina sobre calidad de negocio ni alcance.
- **No** es un producto que aprenda solo: toda regla debe quedar escrita en [[CLAUDE]] y en la bitácora, nunca inferida implícitamente entre sesiones.

---

## 4. Principios rectores (restricciones duras)

No se negocian durante la implementación. Si alguno debe cambiar, primero se registra la decisión en [[BITACORA-DECISIONES]].

| ID | Principio | Regla operativa |
| :---: | :--- | :--- |
| P1 | Un proyecto, una wiki | Cero referencias cruzadas entre proyectos distintos. |
| P2 | Cero dependencias externas | Solo markdown nativo y el agente. Sin plugins de Obsidian, sin scripts. |
| P3 | Un solo escritor | El PO y el agente escriben; el equipo lee. |
| P4 | La wiki compila, no acumula | Si una fuente no aporta sustancia, no genera página nueva. |
| P5 | Ante conflicto, se detiene y pregunta | El agente nunca elige entre dos versiones de un dato ni corrige sin aprobación. |
| P6 | Todo en español | Contenido, plantillas, nombres de archivo y ejemplos en español. |
| P7 | El Excel conserva el detalle de horas | La wiki lleva un campo de corte comparable, no el detalle contable por área. |
| P8 | Alcance por requerimiento | HU, Flujo y WS pertenecen a un solo requerimiento. |
| P9 | La fuente del cliente es inmutable | La solicitud original nunca se modifica. |
| P10 | Economía de contexto | Lectura en cascada (índice → log → resumen → detalle), nunca escaneo completo innecesario. |
| P11 | Mínimo número de documentos | No se crea documento si un campo o fila resuelve la necesidad. Cada carpeta tiene README actualizado. |

---

## 5. Modelo de datos (resumen — fuente normativa completa en [[ONTOLOGIA]])

**7 entidades de primer nivel**, jerarquía estricta de 5 niveles:

```
Requerimiento (1:N) → Flujo (1:N) → Paso de Flujo (1:N) → Historia de Usuario (1:N) → Regla de Negocio
                                          │
                                          └─ (0:N) Web Service
```

| Entidad | Prefijo canónico | Vive como |
| :--- | :--- | :--- |
| Requerimiento | `[SIGLA]-REQ-NNN` | Carpeta propia |
| Seguimiento (documento centralizador) | `seguimiento-[sigla-req].md` | 1 archivo por requerimiento (P11) |
| Historia de Usuario | `HU-[SIGLA]-NNN` | Archivo propio |
| Web Service | `WS-[SIGLA]-NNN` | Archivo propio; `id_proveedor` aparte si viene de un tercero (DP-27) |
| Regla de Negocio | `RN-[SIGLA]-NN` | Ficha dentro de HU o WS |
| Stopper | `STP-[SIGLA]-NN` | Fila en Seguimiento — nunca archivo propio (DEC-12) |
| Paso de Flujo | `P-NN` | Ficha dentro del Flujo |
| Sprint (opcional) | `SPR-NN` | Campo de la Tarea — nunca archivo propio (DEC-11) |

Reglas de negocio completas, cardinalidades exactas y el diagrama Mermaid ER: **ver [[ONTOLOGIA]] §1-3.** Modelo de fases, tarea y stopper: **ver [[MODELO-REQUERIMIENTO]].** Frontmatter obligatorio por tipo de documento: **ver [[ESTANDAR-FRONTMATTER-Y-FECHAS]].**

### 5.1 Vocabularios cerrados

- **Estado de fase:** `No iniciada` · `En curso` · `Bloqueada` · `Completada`
- **Estado macro** (derivado, nunca escrito a mano): `Sin iniciar` · `En curso` · `Bloqueado` · `Cerrado en Producción (Dormido)`
- **Impacto de stopper:** `Crítico` · `Alto` · `Medio` · `Bajo`
- **Estado de stopper:** `Activo` · `Escalado` · `Resuelto`
- **Estado de definición de WS:** `pendiente-proveedor` · `en-contrato` · `disponible` · `deprecado` ([[REGLA-IDENTIFICADOR-WS]] §4.1)

### 5.2 Estructura y fronteras cerradas de Bloque 2

- **Estructura de la Historia de Usuario:** [[plantilla-historia-de-usuario]].
- **Frontera HU ↔ WS:** la HU solo referencia el ID canónico del WS; el detalle técnico vive en la ficha del WS ([[ONTOLOGIA]] §5.6).
- **Tabla de trazabilidad:** vive en [[plantilla-seguimiento-requerimiento]].

No quedan vocabularios abiertos en el modelo. Si en el futuro se necesita uno nuevo, el agente pregunta primero al PO y usa el marcador único `[PENDIENTE]` (ver [[ESTANDAR-FRONTMATTER-Y-FECHAS]] §2.1) hasta que el PO lo cierre explícitamente. Nunca inventa el valor (P5).


---

## 6. Convenciones de escritura (resumen — completo en [[CONVENCIONES-ESCRITURA]])

Frases cortas y afirmativas. Negrita solo en el concepto clave. Tablas para datos, prosa para razonamiento. Máximo 3 niveles de encabezado. Supuestos marcados con `[SUPUESTO]`. Nunca repetir lo que ya vive en otra página — enlazar.

---

## 7. Casos de aceptación

Formato **Dado / Cuando / Entonces**, en español (P6). Cada caso referencia el criterio de éxito que valida (sección 2) y, cuando aplica, la tarea del backlog que lo implementa.

### Funcionalidad 1 — Reporte de pendientes del día

**CP-01 — Reporte del día**
Dado un proyecto con requerimientos activos,
Cuando el PO pregunta "¿qué tenemos pendiente hoy?",
Entonces el agente responde con tareas activas, vencidas, stoppers activos y vacíos detectados, en menos de un minuto de lectura, sin abrir ningún documento adicional.

**CP-15 — Soporte sobre requerimiento cerrado**
Dado un requerimiento en estado "Cerrado en Producción (Dormido)",
Cuando llega una actividad de soporte nueva,
Entonces el agente la registra como seguimiento nuevo dentro del mismo requerimiento, sin duplicarlo y sin borrar ni sobrescribir su documento de conclusión.

### Funcionalidad 2 — Cálculo de avance

**CP-02 — Avance con datos**
Dado un requerimiento con corte de horas registrado,
Cuando el PO pregunta el avance,
Entonces el agente calcula horas ejecutadas sobre estimadas, cita la fuente y declara la fecha del corte.

**CP-03 — Avance sin datos**
Dado un requerimiento sin corte de horas registrado,
Cuando el PO pregunta el avance,
Entonces el agente declara el dato como faltante y NO estima el avance por su cuenta.

### Funcionalidad 3 — Resumen semanal

**CP-04 — Resumen semanal**
Dado un log con entradas de la última semana,
Cuando el PO pide los principales avances,
Entonces el agente construye el resumen desde el log, con cada afirmación rastreable a una entrada concreta.

### Funcionalidad 4 — Detección de contradicciones y propagación

**CP-05 — Propagación de un cambio**
Dado un cambio de definición que afecta a tres documentos,
Cuando el PO lo entrega,
Entonces el agente identifica los tres, pide una sola confirmación y actualiza los tres en una operación.

**CP-06 — Propagación con duda**
Dado un cambio donde un cuarto documento podría o no estar afectado,
Cuando el agente evalúa el impacto,
Entonces lista lo cierto y señala aparte lo dudoso, para que el PO decida.

**CP-07 — Contradicción intra-requerimiento**
Dado una diferencia sembrada entre la HU y el flujo del mismo requerimiento,
Cuando el agente audita,
Entonces la detecta, explica el impacto y NO la corrige por su cuenta.

**CP-08 — Contradicción inter-requerimiento**
Dado el mismo servicio documentado en dos requerimientos con supuestos distintos,
Cuando el agente audita ambos,
Entonces detecta la divergencia y reporta las ubicaciones exactas.

**CP-09 — Falso positivo**
Dado dos textos con el mismo significado y redacción distinta,
Cuando el agente los compara,
Entonces NO reporta contradicción.

**CP-10 — Desactualización**
Dado un log con una definición más reciente que la de la HU,
Cuando el agente los compara,
Entonces clasifica el caso como desactualización (no contradicción) y propone actualizar el dato viejo.

**CP-17 — Trazabilidad incompleta**
Dado que se elimina deliberadamente una fila de la tabla de trazabilidad,
Cuando el agente intenta propagar un cambio,
Entonces la verificación de integridad lo detecta y lo reporta antes de propagar.

### Funcionalidad 5 — Auditoría de rol

**CP-11 — Auditoría de rol**
Dado un Web Service al que se le quitó el propósito funcional,
Cuando el agente recorre el flujo simulando un usuario,
Entonces encuentra el vacío, explica por qué importa y NO inventa el contenido faltante.

### Casos transversales (aplican a todas las funcionalidades)

**CP-12 — Nota sin sustancia**
Dado una nota sin objetivo, actor, regla ni decisión,
Cuando se intenta ingestar,
Entonces el agente propone refinar o descartar, y NO crea página nueva.

**CP-13 — Destino ambiguo**
Dado una nota que podría pertenecer a dos requerimientos,
Cuando se intenta ingestar,
Entonces el agente pregunta antes de escribir y no asume el destino.

**CP-14 — Consulta de requerimiento cerrado**
Dado un requerimiento cerrado en producción,
Cuando el PO pregunta por él,
Entonces el agente responde desde su documento de conclusión, sin abrir el detalle interno completo.

**CP-16 — Integridad estructural**
Dado una página vacía, un enlace roto y un stopper sin responsable, sembrados a propósito,
Cuando el agente ejecuta el chequeo de integridad,
Entonces los tres hallazgos aparecen en el reporte y el agente no corrige ninguno sin permiso.

**CP-18 — Sesión nueva sin contexto**
Dado un agente en una sesión limpia, sin historial previo,
Cuando se le pide ejecutar una ingesta con propagación leyendo solo [[CLAUDE]],
Entonces ejecuta el protocolo completo sin instrucciones adicionales del PO.

**CP-19 — Arranque de proyecto nuevo**
Dado un proyecto de software nuevo,
Cuando se sigue solo el checklist de arranque,
Entonces el proyecto queda operativo sin improvisar ni consultar conversaciones anteriores.

**CP-20 — Agnosticidad**
Dado un proyecto de software de naturaleza distinta al que inspiró el diseño,
Cuando se instancia el sistema sobre él,
Entonces ninguna plantilla exige campos que solo tienen sentido en el proyecto original.

---

## 8. Qué NO debe hacer quien implemente este spec

Ver "Reglas duras de comportamiento del agente" en [[CLAUDE]] — fuente única, no se repite aquí (P11).

---

## 9. Trazabilidad de este documento

Este spec consolida documentos ya aprobados y el protocolo operativo vigente de [[CLAUDE]]. Cualquier cambio de comportamiento se escribe primero en [[CLAUDE]] (o en el documento normativo fuente correspondiente, [[ONTOLOGIA]]/[[MODELO-REQUERIMIENTO]]/etc.), se registra como fila nueva en [[BITACORA-DECISIONES]], y solo después se refleja aquí si aplica.
