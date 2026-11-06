---
id_documento: PLANTILLA-SEGUIMIENTO-B1
tipo_documento: plantilla
bloque: Bloque 1 - Modelo de requerimiento
principios_aplicados:
  - P1
  - P4
  - P7
  - P8
  - P10
  - P11
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-27
estado: Aprobado
---

<!-- DEC-60: banner "Estado actual" agregado para visibilidad inmediata al abrir el documento. -->

# Documento Centralizador de Seguimiento — [SIGLA]-REQ-[NNN]

> **Estado actual:** `[Frase de una línea — Estado Macro + fase activa + siguiente acción. Ej. "Bloqueado — esperando credenciales de Infraestructura para continuar el modelo de datos."]`

Documento único por requerimiento. Aquí viven **todas** las tareas, pendientes y stoppers. No existe documento por tarea ni por bloqueo.

**Regla de visibilidad:** la línea "Estado actual" es lo primero que debe leerse al abrir este documento — se actualiza en cada sesión que toque este requerimiento, junto con la Fecha de Última Actualización.

La definición de cada campo, estado y regla está en `MODELO-REQUERIMIENTO.md`. Este documento no la repite.

---

## Cabecera

| Campo | Valor |
| :--- | :--- |
| **Código del Requerimiento** | `[SIGLA]-REQ-[NNN]` (ej. `DEMO-REQ-001`) |
| **Nombre** | `[Nombre del requerimiento]` |
| **Responsable** | `[Nombre del PO]` |
| **Naturaleza** | `[Desarrollo / Soporte]` |
| **Estado Macro** | `[Derivado de las fases — ver MODELO-REQUERIMIENTO.md §1.3]` |
| **Fecha de Última Actualización** | `[AAAA-MM-DD]` |
| **Hoja principal** | `[[plantilla-hoja-principal-requerimiento]]` |

---

## Control de horas y avance

Tabla única del requerimiento. El detalle contable por área permanece en el Excel (P7).

| Métrica | Valor |
| :--- | :--- |
| **Horas Estimadas Totales** | `0.0 hrs` |
| **Horas Consumidas Totales** | `0.0 hrs` |
| **Balance** | `0.0 hrs` |
| **Porcentaje de Avance** | `0 %` |
| **Fecha de Corte de Horas** | `[AAAA-MM-DD]` |
| **Stoppers Activos** | `0` |

**Regla de vigencia del dato (mitiga R-06):** si la Fecha de Corte tiene más de 7 días respecto a la Fecha de Última Actualización, el agente antepone esta advertencia a cualquier respuesta de avance:

> *El porcentaje de avance puede no ser confiable: el corte de horas es del `[fecha]`.*

El agente **nunca estima el avance por su cuenta**. Si no hay corte registrado, declara el dato como faltante.

---

## Avance por fase

| Fase | Horas Estimadas | Horas Consumidas | Estado |
| :--- | :---: | :---: | :--- |
| **1. REQUERIMIENTO** | `0.0` | `0.0` | `[Estado]` |
| **2. DISEÑO** | `0.0` | `0.0` | `[Estado]` |
| **3. DESARROLLO** | `0.0` | `0.0` | `[Estado]` |
| **4. QA** | `0.0` | `0.0` | `[Estado]` |
| **5. PRODUCCIÓN** | `0.0` | `0.0` | `[Estado]` |

- **Fase activa:** `[Fase]`
- **Siguiente acción:** `[Tarea inmediata para continuar el flujo]`

---

## Registro de stoppers

Responde a *"¿qué está bloqueado, esperando a quién y desde cuándo?"*.

**Sin responsable externo no se admite el registro.**

| ID | Tarea (EDT) | Qué está bloqueado | Motivo | Responsable Externo | Fecha Origen | Antigüedad | Impacto | Estado |
| :---: | :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| `STP-01` | `[EDT]` | `[Entregable detenido]` | `[Causa raíz]` | `[Nombre y área]` | `[AAAA-MM-DD]` | `[N días]` | `[Impacto]` | `[Estado]` |

---

## Tabla de trazabilidad

Punto de falla único del producto (R-01, DP-26, cierra B2-T10). Sin esta tabla no funcionan ni la propagación de cambios (Bloque 4) ni la auditoría de rol (Funcionalidad 5). Documento dueño único: esta tabla no se repite en la hoja principal ni en ningún otro documento (DEC-25).

Una fila por Historia de Usuario. Si un paso de flujo no tiene HU asociada (ej. un paso puramente técnico), se registra igual con `—` en la columna HU.

| Requerimiento | Flujo | Paso | HU | WS | RN | Tarea (EDT) |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: |
| `[SIGLA]-REQ-[NNN]` | `[[nombre-del-flujo]]` | `P-01` | `[[hu-sigla-nnn-nombre]]` | `[[ws-sigla-nnn-nombre]]` | `RN-01, RN-02` | `1.1` |

**Regla de verificación:** si se elimina una fila de esta tabla sin eliminar la HU/WS que describe, la verificación de integridad (Bloque 4) debe detectarlo y reportarlo antes de propagar cualquier cambio (CP-17).

---

## Registro de tareas

Una fila por tarea. Toda tarea declara su fase.

**Diseño confirmado (DEC-29):** una sola tabla con columna `Fase`, en vez de 5 tablas separadas (una por fase). Se prefirió así porque permite ver todo el backlog del requerimiento en una sola lectura, sin perder ninguna tarea entre secciones.

| ID (EDT) | Tarea | Detalle | Fase | Estado | Horas (Est/Cons) | Fecha Límite | Fecha Real | Hito | Notas | Bloqueante |
| :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- | :---: |
| `1.1` | `[Tarea]` | `[Alcance]` | `1. REQUERIMIENTO` | `[Estado]` | `0.0 / 0.0` | `[Fecha]` | `-` | `[Hito]` | `[Notas]` | `Ninguno` |

---

## Bitácora del requerimiento

Registro de cada sesión en que el agente actualizó este requerimiento (DEC-55). No es la bitácora de arquitectura (`BITACORA-DECISIONES.md`) — esa es solo para decisiones de diseño del producto. Esta es el rastro operativo de este requerimiento puntual.

| Fecha | Qué se actualizó | Documentos afectados | Solicitado por |
| :---: | :--- | :--- | :--- |
| `[AAAA-MM-DD]` | `[Resumen en una línea del cambio]` | `[[seguimiento-...]], [[hu-...]]` | `PO` |

**Regla de uso:** una fila por sesión con cambios reales sobre este requerimiento. Una sesión de solo consulta (sin escritura) no genera fila.

---

## Ejemplo de referencia

Instancia ficticia y genérica, conforme a DEC-16. No corresponde a ningún cliente real.

> **Estado actual:** Bloqueado — esperando credenciales del ambiente de pruebas para continuar el modelo de datos de disponibilidad.

**Requerimiento:** `DEMO-REQ-001 — Módulo de Reserva de Salas`
**Naturaleza:** Desarrollo · **Estado Macro:** Bloqueado · **Última actualización:** 2026-07-25

| Métrica | Valor |
| :--- | :--- |
| Horas Estimadas Totales | `86.0 hrs` |
| Horas Consumidas Totales | `31.5 hrs` |
| Balance | `54.5 hrs` |
| Porcentaje de Avance | `37 %` |
| Fecha de Corte de Horas | `2026-07-25` |
| Stoppers Activos | `1` |

**Stoppers**

| ID | Tarea (EDT) | Qué está bloqueado | Motivo | Responsable Externo | Fecha Origen | Antigüedad | Impacto | Estado |
| :---: | :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| `STP-01` | `2.2` | Modelo de datos de disponibilidad | Faltan credenciales del ambiente de pruebas | Infraestructura — A. Rivera | 2026-07-15 | 10 días | Crítico | Activo |

**Trazabilidad**

| Requerimiento | Flujo | Paso | HU | WS | RN | Tarea (EDT) |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: |
| `DEMO-REQ-001` | Flujo principal de reserva | `P-01` | `HU-DEMO-001` | `WS-DEMO-001` | `RN-01` | `3.1` |

**Tareas**

| ID (EDT) | Tarea | Detalle | Fase | Estado | Horas (Est/Cons) | Fecha Límite | Fecha Real | Hito | Notas | Bloqueante |
| :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- | :---: |
| `1.1` | Recepción de solicitud | Registro de la solicitud formal del área usuaria | 1. REQUERIMIENTO | Completada | `6.0 / 6.0` | 2026-07-02 | 2026-07-02 | Solicitud archivada | Fuente inmutable registrada | Ninguno |
| `1.2` | Elicitación de reglas | Levantamiento de reglas de cupo y cancelación | 1. REQUERIMIENTO | Completada | `8.0 / 8.0` | 2026-07-05 | 2026-07-06 | Entendimiento aprobado | Definidas RN-01 y RN-02 | Ninguno |
| `2.1` | Diseño de pantallas | Recorrido de reserva y confirmación | 2. DISEÑO | Completada | `12.0 / 12.0` | 2026-07-12 | 2026-07-12 | Diseño aprobado | Aprobado por el área usuaria | Ninguno |
| `2.2` | Modelo de datos | Esquema de salas, franjas y reservas | 2. DISEÑO | Bloqueada | `10.0 / 5.5` | 2026-07-18 | `-` | Modelo de datos | Detenida por credenciales | `STP-01` |
| `3.1` | Servicio de disponibilidad | Consulta de franjas libres por sala | 3. DESARROLLO | No iniciada | `18.0 / 0.0` | 2026-07-30 | `-` | Servicio en desarrollo | Inicia al liberar el modelo | `STP-01` |
| `4.1` | Matriz de pruebas | Casos funcionales de RN-01 y RN-02 | 4. QA | No iniciada | `12.0 / 0.0` | 2026-08-06 | `-` | Suite de pruebas | — | Ninguno |
| `5.1` | Despliegue | Salida a producción y verificación inicial | 5. PRODUCCIÓN | No iniciada | `10.0 / 0.0` | 2026-08-14 | `-` | Salida a producción | Ventana por acordar | Ninguno |

---

## Reglas de uso

1. **Al instanciar la plantilla se elimina la sección "Ejemplo de referencia".** Si se deja, el documento queda con dos tablas de horas y reintroduce el defecto que esta versión corrigió.
2. **Todo cambio actualiza la Fecha de Última Actualización.** Sin ella la antigüedad de los stoppers deja de ser confiable.
3. **El Estado Macro no se escribe a mano.** Se deriva de las fases (`MODELO-REQUERIMIENTO.md` §1.3).
4. **Las secciones vacías se omiten**, no se dejan con marcadores sin llenar (P11).
5. **Este documento no describe Historias de Usuario, flujos ni Web Services.** Esos artefactos se definen en el Bloque 2 y se enlazan desde la hoja principal.
6. **La tabla de trazabilidad se actualiza en cada HU nueva.** Ninguna HU se considera completa sin su fila correspondiente.
7. **Toda sesión que modifique este requerimiento agrega una fila a la Bitácora del requerimiento y actualiza el banner "Estado actual"**. El agente nunca aplica un cambio en silencio.
