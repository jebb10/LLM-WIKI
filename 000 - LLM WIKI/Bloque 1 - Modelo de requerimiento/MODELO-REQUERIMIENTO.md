---
id_documento: MODELO-REQUERIMIENTO-B1
tipo_documento: norma-contenido
bloque: Bloque 1 - Modelo de requerimiento
principios_aplicados:
  - P1
  - P4
  - P6
  - P7
  - P8
  - P9
  - P10
  - P11
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-28
estado: Aprobado
---

# Modelo de Contenido del Requerimiento

Documento normativo. Define **qué debe contener todo requerimiento** del proyecto, con independencia de su dominio o naturaleza.

No es una plantilla para llenar. Las plantillas que instancian este modelo son `plantilla-hoja-principal-requerimiento.md` y `plantilla-seguimiento-requerimiento.md`.


---

## 1. Las 5 fases de ejecución

Todo requerimiento se ejecuta en cinco fases fijas y en este orden. No se crean fases nuevas ni se omiten fases.

| # | Fase | Qué ocurre en ella |
| :---: | :--- | :--- |
| 1 | **REQUERIMIENTO** | Recepción de la solicitud del cliente, elicitación y entendimiento. |
| 2 | **DISEÑO** | Modelado funcional y técnico de la solución. |
| 3 | **DESARROLLO** | Construcción de la solución. |
| 4 | **QA** | Verificación funcional, integración y corrección de defectos. |
| 5 | **PRODUCCIÓN** | Despliegue, verificación en producción y cierre formal. |

### 1.1 Control de horas por fase

Cada fase registra tres datos: **horas estimadas**, **horas consumidas** y **estado de la fase**.


### 1.2 Estados de fase

Vocabulario cerrado. No se admiten variantes de redacción.

`No iniciada` · `En curso` · `Bloqueada` · `Completada`

### 1.3 Regla de derivación del Estado Macro

El **Estado Macro** del requerimiento no se escribe a mano: se deriva de las fases.

1. Si alguna fase está `Bloqueada`, el Estado Macro es **Bloqueado**, sin importar si una fase posterior está `En curso`. Bloqueada siempre tiene prioridad .
2. Si no hay fases bloqueadas y alguna está `En curso`, el Estado Macro es **En curso**, nombrando la primera fase activa.
3. Si todas las fases están `Completada`, el Estado Macro es **Cerrado en Producción (Dormido)**.
4. Si todas las fases están `No iniciada` (ninguna Bloqueada, En curso ni Completada), el Estado Macro es **Sin iniciar** — regla agregada  (2026-07-28) para cerrar el vacío que dejaban las reglas 1-3 cuando el requerimiento aún no arranca ningún trabajo.

Vocabulario cerrado del Estado Macro:

`En curso` · `Bloqueado` · `Cerrado en Producción (Dormido)` · `Sin iniciar`

**Fuera de alcance de este bloque:** "Pausado por Cliente" no es un valor de Estado Macro. Una pausa del cliente se registra como stopper  y hace que la fase activa quede `Bloqueada`, lo que ya deriva el Estado Macro a `Bloqueado` con la regla 1. La agrupación visual "Pausado por Cliente" es un criterio del índice del proyecto , que se construye leyendo el motivo del stopper — no un campo adicional aquí.

---

## 2. La tarea como unidad de registro

Toda actividad del requerimiento se registra como **fila** en el documento centralizador de seguimiento. No existe documento por tarea (P11).

Ninguna tarea queda huérfana: toda tarea declara siempre su **fase** y pertenece siempre a **un solo requerimiento**.

### 2.1 Campos de la tarea

| # | Campo | Regla |
| :---: | :--- | :--- |
| 1 | **ID (EDT)** | Identificador jerárquico sincronizado con la Estructura de Desglose del Trabajo del cronograma (ej. `2.1`, `5.14`). |
| 2 | **Tarea** | Nombre corto de la actividad. |
| 3 | **Detalle** | Alcance funcional o técnico. |
| 4 | **Fase** | Una de las 5 fases. Obligatorio. |
| 5 | **Estado** | Uno de los 4 estados de fase. Obligatorio. |
| 6 | **Horas (Est / Cons)** | Corte comparable, no detalle contable (P7). |
| 7 | **Fecha Límite** | Formato `AAAA-MM-DD`. |
| 8 | **Fecha Real** | Formato `AAAA-MM-DD`, o `-` si sigue abierta. |
| 9 | **Hito** | Entregable que valida la tarea. Es un **campo**, nunca una entidad ni un documento (DEC-11). |
| 10 | **Notas** | Reglas de negocio, decisiones y responsable interno. |
| 11 | **Bloqueante Asociado** | ID de stopper (`STP-NN`) o `Ninguno`. Prohibido referenciar aquí el ID de otra tarea. |

### 2.2 Sprint

El uso de sprints es **opcional**. Si el proyecto los adopta, el sprint se registra como un **campo adicional de la tarea**, con el formato `SPR-NN`. No genera documento ni entidad propia, por el mismo criterio aplicado al hito (P11). 

---

## 3. El stopper como unidad de bloqueo

Un **stopper** es un bloqueante rastreable con responsable externo y antigüedad. Responde a la pregunta *"¿qué está bloqueado, esperando a quién y desde cuándo?"*.

Como la tarea, vive como **fila** del documento centralizador. No genera documento propio

### 3.1 Campos del stopper

| # | Campo | Regla |
| :---: | :--- | :--- |
| 1 | **ID Bloqueo** | Formato `STP-NN`, correlativo por requerimiento. |
| 2 | **ID Tarea Afectada** | ID EDT de la tarea detenida. |
| 3 | **Qué está bloqueado** | Entregable o actividad detenida. |
| 4 | **Motivo** | Causa raíz del impedimento. |
| 5 | **Responsable Externo** | Persona, proveedor o área cliente. **Obligatorio.** |
| 6 | **Fecha de Origen** | Formato `AAAA-MM-DD`. |
| 7 | **Antigüedad (Días)** | Calculada, no escrita a mano. |
| 8 | **Impacto** | `Crítico` · `Alto` · `Medio` · `Bajo`. |
| 9 | **Estado** | `Activo` · `Escalado` · `Resuelto`. |

### 3.2 Reglas de gestión

- **Sin responsable externo no hay stopper.** Un bloqueo sin responsable no es gestionable y no se registra.
- **Antigüedad calculada:** `Fecha de Última Actualización − Fecha de Origen`. Si el stopper pasa a `Resuelto`, la antigüedad se congela en la fecha de resolución.
- **Un stopper puede afectar a varias tareas.** Se referencia desde cada una en el campo `Bloqueante Asociado`.

---

## 4. Naturaleza del requerimiento

Todo requerimiento declara su naturaleza: **desarrollo** o **soporte**.

| Naturaleza | Qué es | Cómo se ejecuta |
| :--- | :--- | :--- |
| **Desarrollo** | Funcionalidad nueva o evolutiva. | Recorre las 5 fases desde el inicio. |
| **Soporte** | Actividad nueva sobre un requerimiento ya cerrado. | Recorre las mismas 5 fases, dentro del requerimiento original. |

### 4.1 Regla de reapertura

Un requerimiento cerrado **no se archiva ni se mueve de carpeta: se duerme**

Una actividad de soporte lo despierta sin duplicarlo y sin reescribir su historia:

1. No se crea un requerimiento nuevo.
2. Las tareas de soporte se agregan al documento centralizador existente, con su fase correspondiente.
3. El documento de conclusión previo **no se borra ni se sobrescribe**. Registra el soporte en su sección de historial.
4. El Estado Macro vuelve a derivarse de las fases mientras el soporte esté activo.

### 4.2 Regla de pausa

Si el cliente detiene el requerimiento:

1. Las tareas **conservan el estado que tenían**. Ninguna se reinicia, borra ni marca como no iniciada.
2. La pausa se registra como **stopper** sobre la tarea o fase activa en ese momento, con el cliente como responsable externo. Así la antigüedad de la pausa queda medida y es escalable, con el mismo mecanismo que cualquier otro bloqueo (§3).
3. La fase afectada pasa a `Bloqueada`. El Estado Macro deriva a `Bloqueado` por la regla 1 de §1.3 — no existe un estado separado para "pausado".
4. Cuando el cliente reactiva el requerimiento, se resuelve el stopper y la fase vuelve a su estado real.

No se crea un valor de Estado Macro adicional para esto (P11): el stopper ya distingue una pausa de cualquier otro bloqueo con su campo `Motivo` y `Responsable Externo`.

---

## 5. Dónde vive cada cosa

Regla de reparto obligatoria. Existe para impedir que el mismo dato se escriba en dos documentos y para que la propagación de cambios (Bloque 4) tenga un destino único por dato.

| Contenido | Documento dueño | Los demás documentos |
| :--- | :--- | :--- |
| Definición de campos, estados y reglas del modelo | `MODELO-REQUERIMIENTO.md` | Referencian, no repiten. |
| Tabla de tareas y tabla de stoppers | `plantilla-seguimiento-requerimiento.md` | Enlazan, no repiten. |
| Resumen ejecutivo, contexto, actores y reglas macro | `plantilla-hoja-principal-requerimiento.md` | Enlazan, no repiten. |
| Solicitud original del cliente | `plantilla-requerimiento-cliente.md` | Referencian. Nunca la transcriben de nuevo. |
| Síntesis final del requerimiento cerrado | `plantilla-conclusion-requerimiento.md` | Enlazan. |

**Verificación:** ningún dato de este modelo debe poder encontrarse descrito con detalle en dos documentos distintos. Si ocurre, hay un defecto de diseño, no una comodidad.

---

## 6. Dónde vive cada definición técnica de Bloque 2

Este modelo (Bloque 1) define la tarea, el stopper y las 5 fases. Las definiciones técnicas de integración, HU y trazabilidad viven en Bloque 2 y este documento no las repite (P4, P11) — solo referencia dónde consultarlas:

| Elemento | Documento normativo |
| :--- | :--- |
| Metadatos (frontmatter) y formato de fechas | [[ESTANDAR-FRONTMATTER-Y-FECHAS]] (DP-08) |
| Identificador estable de Web Service | [[REGLA-IDENTIFICADOR-WS]] (DP-21) |
| Granularidad y vocabulario de estados de WS | [[REGLA-IDENTIFICADOR-WS]] (DP-22, DP-23) |
| Contrato mínimo de información de un WS | [[plantilla-contrato-ws]] (DP-01) |
| Plantilla de Historia de Usuario | [[plantilla-historia-de-usuario]] (DP-25, DP-28, DP-30) |
| Plantilla de Flujo funcional y pasos (`P-01`…) | [[plantilla-flujo-funcional]] |
| Frontera entre HU y WS | [[ONTOLOGIA]] §5.6 (DP-29) |
| Tabla de trazabilidad y enlaces obligatorios | [[plantilla-seguimiento-requerimiento]] § Tabla de trazabilidad (DP-26) |
| Sigla del requerimiento y nomenclatura | [[ONTOLOGIA]] (DP-10, DP-27) |
| Glosario del proyecto | [[GLOSARIO]] |
