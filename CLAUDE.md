# CLAUDE.md

Este archivo es la versión **definitiva** de instrucciones para el agente y es la **fuente de verdad vigente** sobre cómo operar en esta bóveda. Reemplaza cualquier borrador anterior.

## Qué es este repositorio

Bóveda de Obsidian (Markdown puro, sin plugins ni scripts — P2) que documenta el diseño y la norma de un producto: un **LLM Wiki con agente** para llevar proyectos de software con trazabilidad total de tareas, definiciones y contradicciones. No es un repositorio de código: no hay build, lint ni tests que ejecutar.

El modelo del producto está **cerrado**: principios, ontología, jerarquía de entidades y las plantillas normativas (ver "Documentos normativos vigentes") ya no se rediseñan. La visión completa vive en `000 - LLM WIKI/Bloque 0 - Gobierno/00-VISION.md` y el historial de decisiones en `000 - LLM WIKI/Bloque 0 - Gobierno/BITACORA-DECISIONES.md`. `SPEC.md` es material fundacional de referencia para entender el proyecto (no se sigue editando en paralelo a este archivo). El protocolo operativo (ingesta, propagación, consulta, integridad, carpetas, empaquetado) es el que describe este documento — no requiere leer material fundacional para operar.

## Cómo arrancar

- **Si eres un agente y esta es tu primera sesión en este repositorio:** lee este archivo completo. Es suficiente — no necesitas ningún otro documento para operar.
- **Para instanciar la wiki sobre un proyecto de software nuevo:** sigue `000 - LLM WIKI/Bloque 0 - Gobierno/CHECKLIST-ARRANQUE-PROYECTO-NUEVO.md`, paso por paso.
- **Para ver el sistema funcionando:** `100 - PROYECTO ACTIVO/` trae `DEMO-REQ-001` instanciado de punta a punta (requerimiento ficticio de reserva de salas) como ejemplo de referencia.
- **Si eres una persona que acaba de clonar el repositorio:** empieza por `README.md` en la raíz.

**Quién es el PO:** la persona que opera la bóveda y decide sobre su contenido — responsable de dar seguimiento a pendientes, tareas, stoppers y proyección de entregas de los requerimientos. El equipo de desarrollo consulta la bóveda para saber qué debe construir el producto — nunca la edita.

`PO` es una **etiqueta de rol, no un cargo**: en este documento y en los 6 subagentes designa siempre a "quien opera y decide sobre la bóveda", sea analista de requerimientos, product owner, project manager, tech lead o un desarrollador trabajando solo. No se renombra en la documentación; se lee como ese único rol operador.

**Punto de partida por requerimiento:** la primera sesión de trabajo sobre **cualquier** requerimiento es una sesión de **ingesta desde cero**, sin importar si la carpeta del requerimiento ya contiene Historia de Usuario, ficha de Web Service o cualquier otro contenido migrado previamente. El agente **no asume que ese contenido existente esté completo, vigente o correcto** — se reconstruye a partir de lo que el PO entregue, siguiendo el protocolo de Ingesta de abajo. El refinamiento sección-por-sección de la plantilla empieza en la sesión siguiente, sobre lo ya ingerido en esa primera sesión.

## Regla de precedencia

Cadena de precedencia: **`CLAUDE.md` > `SPEC.md` > `BITACORA-DECISIONES.md`**. Este `CLAUDE.md` es la **fuente de verdad vigente** sobre cómo debe operar el agente. `SPEC.md` es material fundacional/histórico para entender el proyecto — ya no se edita como documento operativo en paralelo a este archivo; si algo en `SPEC.md` contradice a `CLAUDE.md`, gana `CLAUDE.md`. `000 - LLM WIKI/Bloque 0 - Gobierno/BITACORA-DECISIONES.md` registra el historial de decisiones nuevas conforme se van tomando, como registro de referencia — no tiene precedencia sobre ninguno de los dos anteriores. Toda decisión nueva confirmada por el PO se escribe directamente aquí, y el agente deja además una fila nueva en la bitácora, al cerrar la sesión en que se tomó, para dejar rastro de cuándo y por qué.

## Los 11 principios rectores (no negociables)

| ID  | Principio                                                                          |
| :-: | :--------------------------------------------------------------------------------- |
| P1  | Un proyecto, una wiki — cero referencias cruzadas entre proyectos.                 |
| P2  | Cero dependencias externas — solo Markdown nativo y el agente.                     |
| P3  | Un solo escritor — el PO y el agente escriben; el equipo lee.                      |
| P4  | La wiki compila, no acumula — sin sustancia, no hay página nueva.                  |
| P5  | Ante conflicto, el agente se detiene y pregunta — nunca elige por su cuenta.       |
| P6  | Todo en español.                                                                   |
| P7  | La wiki lleva un corte comparable de Requerimientos.                               |
| P8  | Alcance por requerimiento — HUs, Flujos y WS pertenecen a un solo requerimiento.   |
| P9  | La fuente del cliente es inmutable.                                                |
| P10 | Economía de contexto — lectura en cascada, nunca escaneo completo.                 |
| P11 | Mínimo número de documentos — un campo o fila resuelve antes que un archivo nuevo. |

Detalle completo en `000 - LLM WIKI/Bloque 0 - Gobierno/00-VISION.md`.

## Modelo de entidades (resumen)

Jerarquía funcional estricta de 5 niveles:

```
Requerimiento (1:N) → Flujo (1:N) → Paso de Flujo (1:N) → Historia de Usuario (1:N) → Regla de Negocio
                                          └─ (0:N) Web Service
```

| Entidad | Prefijo canónico | Vive como |
| :--- | :--- | :--- |
| Requerimiento | `[SIGLA]-REQ-NNN` | Carpeta propia |
| Seguimiento | `seguimiento-[sigla-req].md` | 1 archivo por requerimiento |
| Historia de Usuario | `HU-[SIGLA]-NNN` | Archivo propio |
| Web Service | `WS-[SIGLA]-NNN` | Archivo propio, **una ficha por endpoint** (`id_proveedor` aparte si es de un tercero) |
| Regla de Negocio | `RN-[SIGLA]-NN` | Ficha dentro de HU o WS |
| Stopper | `STP-[SIGLA]-NN` | Fila en Seguimiento, nunca archivo propio |
| Paso de Flujo | `P-NN` | Ficha dentro del Flujo (diagrama Mermaid) |
| Sprint (opcional) | `SPR-NN` | Campo de la Tarea, nunca archivo propio |

Sigla mínima de 4 letras mayúsculas. Modelo normativo completo, cardinalidades y diagrama ER: `000 - LLM WIKI/Bloque 2 - Ontología y relaciones/ONTOLOGIA.md`. Fases, tarea y stopper: `000 - LLM WIKI/Bloque 1 - Modelo de requerimiento/MODELO-REQUERIMIENTO.md`.

## Reglas duras de comportamiento del agente

- **Nunca inventar valores** de un vocabulario cerrado. Todos los vocabularios del modelo (estados de fase, Estado Macro, impacto/estado de stopper, estado de definición de WS) están cerrados — ver `ONTOLOGIA.md`, `MODELO-REQUERIMIENTO.md` y `REGLA-IDENTIFICADOR-WS.md`.
- **Nunca crear un documento nuevo** por tarea, stopper, hito o sprint — son filas o campos del documento de Seguimiento (P11).
- **Nunca resolver una contradicción ni corregir un hallazgo de integridad** sin aprobación explícita del PO (P5).
- **Nunca usar rutas absolutas** (`file:///...`) para enlazar documentos — usar wikilinks `[[NombreDocumento]]` nativos de Obsidian (P2).
- **Nunca escribir URLs ni detalle técnico de un Web Service** en una HU, Paso de Flujo o Regla de Negocio — solo su ID canónico. El detalle vive únicamente en la ficha del WS.
- **Nunca usar datos reales de cliente** en ejemplos, demos o plantillas normativas — siempre ficticios y genéricos, con la sigla unificada `DEMO`.
- **Este repositorio es publicable.** Nunca lleva datos reales de cliente: ni nombres de empresa, ni personas, ni URLs de servicios reales, ni rutas absolutas de una máquina concreta. Todo dato de ejemplo es ficticio. Si el PO trae información de un proyecto real, vive en su propia copia privada de esta bóveda — nunca en la versión que se publica.
- El agente **ejecuta y mantiene la wiki; no opina** sobre calidad de negocio ni alcance.

## Convención de nombres de archivo

| Tipo de documento | Convención | Ejemplo |
| :--- | :--- | :--- |
| Normativo (regla de arquitectura, técnica o de estilo) | `MAYUSCULAS-CON-GUIONES.md` | `ONTOLOGIA.md`, `REGLA-IDENTIFICADOR-WS.md` |
| Plantilla (molde a instanciar) | `plantilla-nombre-en-minusculas.md` | `plantilla-seguimiento-requerimiento.md` |
| Ficha instanciada de un requerimiento real | `tipo-sigla-nnn-nombre.md`, todo en minúsculas | `hu-demo-001-reservar-sala.md` |
| Fuente de cliente (inmutable, P9) | Se conserva el nombre de origen; solo se limpia el sufijo de conversión (`.docx.md` → `.md`) | `Manual de Diligenciamiento Formato Historia de Usuario v.2.md` |
| Consolidador de familia | `consolidado-familia-[sigla].md`, en la raíz de la carpeta `[SIGLA]-FAMILIA/` | `consolidado-familia-acro.md` |
| Índice temático de Web Services (requerimiento con muchos WS) | `indice-ws-[sigla]-req-[nnn].md` | `indice-ws-demo-req-001.md` |
| Reporte de subagente (estado de la corrida más reciente) | `reporte-actual.md`, en `Bloque 0 - Gobierno/agentes/` | `reporte-actual.md` |
| Log de subagentes (histórico append-only de corridas) | `historico-auditorias.md`, en `Bloque 0 - Gobierno/agentes/` | `historico-auditorias.md` |

Excepciones que no se renombran:

- Los 3 archivos `LEEME-*.md` de `Bloque 0-2` (`LEEME-GOBIERNO.md`, `LEEME-MODELO-DE-REQUERIMIENTO.md`, `LEEME-ONTOLOGIA-Y-RELACIONES.md`) son índices propios de cada bloque, deliberadamente nombrados así en vez de con la convención normativa `MAYUSCULAS-CON-GUIONES.md`.
- `00-VISION.md` conserva su prefijo numérico `00-` por ser el punto de entrada de `Bloque 0 - Gobierno/`, aunque sea un documento normativo.

**`_fuente-cliente/` es opcional:** solo existe cuando el requerimiento tuvo un documento original de cliente, puede que haya requerimientos sin este documento.

## Estructura de la raíz

La bóveda tiene **dos espacios hermanos**, en una sola bóveda de Obsidian (un solo `.obsidian` en la raíz):

- `000 - LLM WIKI/` — **guía del agente**: contenedor de los 3 bloques normativos.
  - `Bloque 0 - Gobierno/` — visión, bitácora de decisiones, convenciones de escritura, checklist de arranque, e [[INDICE-DOCUMENTOS-GUIA]] (relación única de todos los documentos de la guía del agente — raíz).
    - `agentes/` — los 2 archivos de salida de los subagentes de auditoría ([[reporte-actual]] e [[historico-auditorias]]); nunca se crea un tercer archivo de reporte aquí (P11, P4).
  - `Bloque 1 - Modelo de requerimiento/` — modelo de contenido del requerimiento y sus 5 plantillas.
  - `Bloque 2 - Ontología y relaciones/` — ontología, estándar de frontmatter/fechas, identificador de WS, plantillas de WS/HU/Flujo, glosario, y la fuente de cliente del manual de HU.
- `100 - PROYECTO ACTIVO/` — **proyecto real en curso**: es el destino del trabajo de refinamiento. Trae `DEMO-REQ-001` instanciado como ejemplo de referencia; al arrancar un proyecto propio se sigue el checklist de arranque.
- `referencias-externas/` — material de inspiración de terceros, no autoría de este proyecto. Fuera del alcance de auditoría.
- `README.md`, `GEMINI.md` y `LICENSE` (raíz) — artefactos del repositorio (portada para lectores humanos, puente ligero multi-agente hacia `CLAUDE.md` y licencia), no páginas de la wiki. Quedan fuera del grafo y del alcance de auditoría a propósito: no se les exige wikilink entrante ni saliente (DEC-08, DEC-10).

**Regla de frontera entre los dos espacios (convención de grafo, no barrera técnica):** un wikilink nunca cruza de la guía del agente al proyecto activo ni al revés. Técnicamente resolvería —es una sola bóveda—, pero rompe la topología de dos grupos separados que diseñó el PO, así que se reporta como hallazgo. La guía describe el molde; el proyecto lo instancia. Se mantienen en una sola bóveda a propósito: así quien clone el repositorio ve el grafo completo de una sola vez, y los subagentes auditan ambos espacios en una sola corrida.

Estructura interna de `100 - PROYECTO ACTIVO/`:

- `001 - Cronograma de Requerimientos/` — los 2 documentos de seguimiento agregado: `000 - Plan de Trabajo - Cronograma de Requerimientos.md` (tablero único de estado de los requerimientos vigentes) y `001 - Requerimientos Cerrados y Pausados.md` (hub de los cerrados/pausados/sin iniciar).
- `002 - Requerimientos/` — agrupa las carpetas de requerimiento (`[SIGLA]-REQ-NNN/`) y el índice plano `INDICE-DOCUMENTOS-REQUERIMIENTOS.md` (relación única — mapa de contenido, sin wikilinks reales — de todos los documentos activos de los requerimientos vigentes; no repite estado, que vive en el cronograma y en cada Seguimiento).
- `_entrada-actualizaciones/` — buzón de intake: aquí el PO deposita HU o notas estructuradas nuevas para que el agente las ingiera en la siguiente sesión del requerimiento correspondiente.
- `004 - Canvas/` y `005 - Files/` — espacio de trabajo propio del PO (mockups, diagramas y adjuntos sueltos); fuera del alcance del agente y de los subagentes de auditoría.

## Documentos normativos vigentes

`00-VISION.md` · `BITACORA-DECISIONES.md` · `CONVENCIONES-ESCRITURA.md` · `CHECKLIST-ARRANQUE-PROYECTO-NUEVO.md` · `MODELO-REQUERIMIENTO.md` · `plantilla-requerimiento-cliente.md` · `plantilla-hoja-principal-requerimiento.md` · `plantilla-seguimiento-requerimiento.md` (incluye la tabla de trazabilidad) · `plantilla-conclusion-requerimiento.md` · `plantilla-mapeo-excepcion-jerarquia.md` · `ONTOLOGIA.md` · `ESTANDAR-FRONTMATTER-Y-FECHAS.md` · `REGLA-IDENTIFICADOR-WS.md` · `plantilla-contrato-ws.md` · `plantilla-historia-de-usuario.md` · `plantilla-flujo-funcional.md` · `GLOSARIO.md`.

No se regeneran ni reinterpretan. `SPEC.md` tiene los 20 casos de aceptación que validan el comportamiento esperado del agente, y resume el protocolo operativo — ambos como referencia fundacional; esta sección de `CLAUDE.md` lo detalla para el día a día y prevalece ante cualquier diferencia.
### Familia de requerimientos (2+ REQ bajo la misma sigla)

Regla para cuando aparezcan siglas con más de un `REQ-NNN` independiente (no jerárquico — cada uno es un requerimiento completo, solo comparten sigla por origen):

- Se agrupan en una carpeta padre `[SIGLA]-FAMILIA/`, conteniendo cada `[SIGLA]-REQ-NNN/` como subcarpeta propia (sin tocar su contenido interno).
- Cada miembro conserva su propia hoja principal (`plantilla-hoja-principal-requerimiento.md`), con una referencia cruzada en su sección 9 a las demás variantes de la familia.
- Un documento único `consolidado-familia-[sigla].md`, en la raíz de la carpeta padre, centraliza estado y navegación de toda la familia — es el documento que usa el PO para seguimiento agregado.
- Si un miembro de la familia sigue activo (no cerrado), su hoja principal se difiere hasta que el PO decida crearla durante su propio refinamiento — no se fuerza solo por pertenecer a una familia ya organizada.
## Cómo operar ahora

### Ingesta

1. **El PO es la única fuente de información nueva.**
2. **Antes de actualizar o retirar cualquier información** (típicamente a partir de una HU o nota que entrega el PO), el agente pregunta explícitamente qué se debe actualizar o retirar. Nunca asume el alcance del cambio.
3. **Ante un dato sin ficha propia** (ej. un Web Service mencionado sin ficha), el agente pregunta antes de crear cualquier documento nuevo — nunca crea por iniciativa propia.
4. **Una sesión de trabajo atiende un solo requerimiento.** No se mezclan expedientes en la misma sesión.
5. **El PO entrega toda la información necesaria** para refinar correctamente el requerimiento (HU o nota original), depositándola en `_entrada-actualizaciones/` antes de la sesión.

### Refinamiento de HU y WS

6. **Leer y escanear completo** → documento de Seguimiento del requerimiento → documentos asociados al requerimiento que se trabaja en la sesión
7. **Al refinar una HU:** seguir `plantilla-historia-de-usuario.md` sección por sección, siempre desde cero según el punto de partida definido arriba. Si falta actor, regla o criterio de aceptación, detenerse y preguntar al PO — no completar por suposición.
8. **El agente solo actualiza los documentos asociados** al requerimiento (Seguimiento, HU, WS, Flujo) — nunca modifica los documentos originales de `_fuente-cliente/` (P9).
9. **Al encontrar un Web Service sin ficha propia o mal referenciado:** crear su ficha con `plantilla-contrato-ws.md`, una por endpoint, y actualizar la tabla de trazabilidad del requerimiento.

### Propagación

10. **La propagación de un cambio se limita al requerimiento afectado**: su documento de Seguimiento y la(s) HU relacionadas que el PO señale. El agente nunca propaga un cambio hacia otro requerimiento sin instrucción expresa del PO.
11. **Si el agente detecta un posible impacto cruzado** hacia otro requerimiento (ej. dos requerimientos que dependen del mismo Web Service), lo reporta como hallazgo y espera indicación — nunca lo aplica por su cuenta.
12. **Toda actualización cierra con un resumen visible al PO** de lo que se modificó, y una fila nueva en la sección "Bitácora del requerimiento" de su documento de Seguimiento. Nunca se aplica un cambio en silencio.

### Consulta

13. Sin reportes automáticos programados. El agente responde preguntas ad-hoc en sesión (pendientes del día, avance por requerimiento, resumen semanal, contradicciones, auditoría de rol recorriendo el flujo como un usuario).
14. `100 - PROYECTO ACTIVO/001 - Cronograma de Requerimientos/000 - Plan de Trabajo - Cronograma de Requerimientos.md` es el único tablero consolidado del estado de los requerimientos vigentes — no se crea un dashboard adicional (P11, P4).

### Integridad y contradicciones

15. **Al detectar una contradicción o un vacío de documentación**, reportarlo de inmediato y de forma explícita — describiendo el conflicto en palabras, no solo citando identificadores — con su ubicación exacta. Nunca corregirlo ni inventar el contenido faltante (P5; ver CP-07, CP-11 en `SPEC.md`).
16. **No hay umbral de "ruido":** toda contradicción de sustancia se reporta, sin excepción.

### Carpetas y plantillas

17. `plantilla-hoja-principal-requerimiento.md` y `plantilla-requerimiento-cliente.md` siguen vigentes; sus instancias por requerimiento se completan durante el refinamiento individual, no antes.
18. `004 - Canvas/` y `005 - Files/` permanecen fuera de wikilinks de las HU por diseño — son el espacio de trabajo de mockups y adjuntos del PO, no artefactos normativos.

### Cierre y empaquetado

19. Un requerimiento se cierra generando su `conclusion-*.md` con `plantilla-conclusion-requerimiento.md` cuando su Estado Macro pasa a `Cerrado en Producción`.
20. **Toda regla nueva de comportamiento** confirmada por el PO se escribe directamente aquí, en `CLAUDE.md`, y se deja además una fila nueva en `BITACORA-DECISIONES.md` como registro histórico.

### Aclaraciones operativas

21. **Ingesta:** llega como documento ya redactado por el PO (no nota suelta), depositado en `_entrada-actualizaciones/` antes de la sesión — el agente lo lee al iniciar esa sesión de ese requerimiento.
22. **Elección de requerimiento:** el PO decide con cuál trabajar al iniciar cada sesión; el agente nunca lo propone.
23. **Stoppers:** solo el PO cambia un stopper de `Activo` a `Escalado`. El agente nunca abre por su cuenta el tema de un stopper "Pausado por Cliente" en sesión de otro requerimiento — solo si el PO lo trae.
24. **Dato faltante:** queda en `[PENDIENTE]` y la sesión sigue sobre el resto de la ficha; no se detiene la ficha completa.
25. **WS repetido dentro del mismo requerimiento:** una sola ficha, referenciada por ID, nunca duplicada.
26. **Un solo operador:** solo el PO opera la bóveda (P3 sin segunda persona autorizada).
27. **Resumen de cierre de sesión:** breve — qué cambió y qué queda pendiente, no un recorrido campo por campo.
28. **Más de 15 RN/CA en una HU real** (límite de plantilla): el agente se detiene y pregunta al PO cómo dividirla — nunca decide la partición solo.
29. **Hoja principal del requerimiento:** se llena en paralelo a medida que aparecen actores y reglas de negocio macro en las HU, no de una sola vez al abrir el requerimiento.
30. **Soporte sobre requerimiento cerrado** (ver CP-15 en `SPEC.md`): fila nueva en su mismo documento de seguimiento, sin tocar la conclusión.
31. **Sigla nueva sin fuente clara:** el agente la propone (mínimo 4 letras) y espera aprobación explícita del PO antes de crear la carpeta.
32. **Estado de WS ambiguo** frente al vocabulario cerrado (`pendiente-proveedor`/`en-contrato`/`disponible`/`deprecado`): el agente se detiene y pregunta cuál aplica — nunca fuerza el valor más cercano (P5).
33. **Auditoría de rol** (ver CP-11 en `SPEC.md`): solo se ejecuta cuando el PO la pide explícitamente; el agente nunca la ofrece por iniciativa propia.

## Subagentes de auditoría

Seis agentes de solo lectura definidos en `.claude/agents/`: 5 auditores (`conexiones-vault`, `organizador-carpetas`, `vista-grafica`, `logica-requerimientos`, `auditoria-de-rol`) y 1 orquestador (`auditoria-completa`). Detectan y describen; ninguno corrige, mueve ni borra nada de la bóveda — su único permiso de escritura es sobre sus dos archivos de salida.

- **Invocación manual únicamente.** El PO los invoca explícitamente por nombre; ninguno se dispara por descripción de tarea ni por iniciativa propia.
- **Los 3 estructurales** (`conexiones-vault`, `organizador-carpetas`, `vista-grafica`) auditan dos espacios siempre por separado: la guía del agente (raíz + `Bloque 0-2`) y el proyecto activo `100 - PROYECTO ACTIVO/` — excluyendo siempre `004 - Canvas/`, `005 - Files/` y `referencias-externas/`.
- **Los 2 de refinamiento** (`logica-requerimientos`, `auditoria-de-rol`) son agnósticos: trabajan sobre un solo requerimiento a la vez, siempre el que el PO indique al invocarlos — nunca lo eligen ni lo asumen de una sesión anterior. `auditoria-de-rol` solo se invoca cuando el PO la pide de forma explícita (regla 33).
- **`auditoria-completa` corre siempre y únicamente** los 3 estructurales, en orden fijo (`conexiones-vault` → `organizador-carpetas` → `vista-grafica`). Nunca incluye a los 2 de refinamiento, aunque el PO no lo aclare — esos se invocan aparte, durante sesiones de refinamiento de un requerimiento puntual.
- **Topología de grafo esperada** (estándar contra el que audita `vista-grafica`): dos grupos separados, sin cruces entre ellos. (1) Guía del agente, enlazada entre sí vía hubs (READMEs, índices, `CLAUDE.md`). (2) Por cada requerimiento, sus HU/WS/Flujo/documentos asociados enlazan solo hacia la hoja principal del requerimiento (texto plano con el ID hacia los demás, nunca wikilink); solo la hoja principal enlaza además hacia la hoja maestra de Seguimiento/cronograma. Ninguna página debe quedar huérfana — si un documento no tiene ninguna relación real, es un hallazgo que el PO decide cómo resolver (conectar o eliminar), nunca algo que el agente resuelva por su cuenta.
- **Única excepción del patrón estrella:** el documento de Seguimiento sí usa wikilinks reales hacia HU, WS y Flujo en su Tabla de trazabilidad y en la columna "Documentos afectados" de su Bitácora — así lo exige `plantilla-seguimiento-requerimiento.md`. Es necesario porque sin esos enlaces navegables no funcionan la propagación de cambios ni la auditoría de rol. `vista-grafica` no reporta esos enlaces como hallazgo.
- **Salida — nunca un archivo de reporte nuevo por corrida (P11, P4):** `000 - LLM WIKI/Bloque 0 - Gobierno/agentes/reporte-actual.md` (una sección fija por agente, se sobrescribe solo la sección del agente que corrió) y `000 - LLM WIKI/Bloque 0 - Gobierno/agentes/historico-auditorias.md` (log append-only, una fila por corrida; si el mismo agente corre dos veces el mismo día, complementa la fila de esa fecha en vez de duplicarla).
- **Prioridad de hallazgo:** `Crítico` rompe una regla dura o bloquea trazabilidad; `Menor` es desviación de forma que no bloquea nada.
- **`auditoria-de-rol` reporta en tres partes** por hallazgo: qué falta, por qué importa, y una sugerencia de cómo resolverlo apoyada solo en la documentación del mismo requerimiento (nunca cruza a otro requerimiento, nunca inventa el valor) — la sugerencia es una propuesta, nunca se aplica sola (P5).
- **Bitácora:** los hallazgos Críticos que ameriten fila nueva en `BITACORA-DECISIONES.md` se proponen solo en el chat de la sesión (por el orquestador o por el agente puntual que corrió) — nunca como tabla fija dentro del reporte, y nunca se escriben sin que el PO apruebe cada fila (P3, P5).

## Convenciones de escritura

Frases cortas y afirmativas, sin preámbulos. Negrita solo en el concepto clave. Tablas para datos, prosa para razonamiento. Máximo 3 niveles de encabezado. Supuestos marcados con `[SUPUESTO]`. Nunca repetir lo que ya vive en otra página — enlazar. Todo en español (P6). Detalle en `000 - LLM WIKI/Bloque 0 - Gobierno/CONVENCIONES-ESCRITURA.md`.
