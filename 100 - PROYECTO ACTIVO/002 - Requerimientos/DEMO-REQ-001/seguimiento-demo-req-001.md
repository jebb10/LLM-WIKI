---
id_documento: SEGUIMIENTO-DEMO-REQ-001
tipo_documento: seguimiento
id_requerimiento_padre: DEMO-REQ-001
fecha_corte_horas: 2026-07-25
horas_estimadas_total: 86.0
horas_consumidas_total: 31.5
stoppers_activos: 1
fecha_actualizacion: 2026-07-29
---

# Documento Centralizador de Seguimiento — DEMO-REQ-001

> **Estado actual:** Bloqueado — esperando credenciales del ambiente de pruebas de Infraestructura para cerrar el modelo de datos de disponibilidad.

Documento único por requerimiento. Aquí viven **todas** las tareas, pendientes y stoppers. No existe documento por tarea ni por bloqueo.

La definición de cada campo, estado y regla está en el Modelo de Requerimiento de la guía del agente. Este documento no la repite.

---

## Cabecera

| Campo | Valor |
| :--- | :--- |
| **Código del Requerimiento** | `DEMO-REQ-001` |
| **Nombre** | Módulo de Reserva de Salas |
| **Responsable** | Nombre del PO |
| **Naturaleza** | Desarrollo |
| **Estado Macro** | `Bloqueado` (derivado de las fases) |
| **Fecha de Última Actualización** | `2026-07-29` |
| **Hoja principal** | [[hoja-principal-demo-req-001]] |

---

## Control de horas y avance

| Métrica | Valor |
| :--- | :--- |
| **Horas Estimadas Totales** | `86.0 hrs` |
| **Horas Consumidas Totales** | `31.5 hrs` |
| **Balance** | `54.5 hrs` |
| **Porcentaje de Avance** | `37 %` |
| **Fecha de Corte de Horas** | `2026-07-25` |
| **Stoppers Activos** | `1` |

El agente **nunca estima el avance por su cuenta**. Si no hay corte registrado, declara el dato como faltante.

---

## Avance por fase

| Fase | Horas Estimadas | Horas Consumidas | Estado |
| :--- | :---: | :---: | :--- |
| **1. REQUERIMIENTO** | `14.0` | `14.0` | `Completada` |
| **2. DISEÑO** | `22.0` | `17.5` | `Bloqueada` |
| **3. DESARROLLO** | `28.0` | `0.0` | `No iniciada` |
| **4. QA** | `12.0` | `0.0` | `No iniciada` |
| **5. PRODUCCIÓN** | `10.0` | `0.0` | `No iniciada` |

- **Fase activa:** `2. DISEÑO`
- **Siguiente acción:** obtener credenciales del ambiente de pruebas para cerrar el modelo de datos de disponibilidad.

---

## Registro de stoppers

| ID | Tarea (EDT) | Qué está bloqueado | Motivo | Responsable Externo | Fecha Origen | Antigüedad | Impacto | Estado |
| :---: | :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| `STP-01` | `2.2` | Modelo de datos de disponibilidad | Faltan credenciales del ambiente de pruebas | Infraestructura — responsable asignado | `2026-07-15` | 14 días | `Crítico` | `Activo` |

---

## Tabla de trazabilidad

Punto de falla único del producto. Sin esta tabla no funcionan ni la propagación de cambios ni la auditoría de rol. Documento dueño único: esta tabla no se repite en la hoja principal ni en ningún otro documento.

| Requerimiento | Flujo | Paso | HU | WS | RN | Tarea (EDT) |
| :--- | :--- | :---: | :--- | :--- | :--- | :---: |
| `DEMO-REQ-001` | [[flujo-demo-001-reserva-de-sala]] | `P-01` | [[hu-demo-001-reservar-sala]] | [[ws-demo-001-consulta-disponibilidad-salas]] | `RN-01` | `3.1` |
| `DEMO-REQ-001` | [[flujo-demo-001-reserva-de-sala]] | `P-02` | — | — | — | `3.1` |
| `DEMO-REQ-001` | [[flujo-demo-001-reserva-de-sala]] | `P-03` | [[hu-demo-001-reservar-sala]] | [[ws-demo-002-crear-reserva]] | `RN-01, RN-02, RN-03, RN-04` | `3.2` |
| `DEMO-REQ-001` | [[flujo-demo-001-reserva-de-sala]] | `P-04` | [[hu-demo-001-reservar-sala]] | — | `RN-01, RN-02` | `3.2` |
| `DEMO-REQ-001` | [[flujo-demo-001-reserva-de-sala]] | `P-05` | [[hu-demo-001-reservar-sala]] | — | — | `3.2` |

`P-02` es un punto de decisión resuelto por el sistema: no tiene HU asociada a propósito, y se registra igual con `—` para no dejar huecos en la trazabilidad.

**Regla de verificación:** si se elimina una fila de esta tabla sin eliminar la HU/WS que describe, la verificación de integridad debe detectarlo y reportarlo antes de propagar cualquier cambio (CP-17).

---

## Registro de tareas

| ID (EDT) | Tarea | Detalle | Fase | Estado | Horas (Est/Cons) | Fecha Límite | Fecha Real | Hito | Notas | Bloqueante |
| :---: | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- | :---: |
| `1.1` | Recepción de solicitud | Registro de la solicitud formal del área usuaria | `1. REQUERIMIENTO` | `Completada` | `6.0 / 6.0` | `2026-07-02` | `2026-07-02` | Solicitud archivada | — | `Ninguno` |
| `1.2` | Elicitación de reglas | Levantamiento de reglas de cupo, anticipación y duración | `1. REQUERIMIENTO` | `Completada` | `8.0 / 8.0` | `2026-07-05` | `2026-07-06` | Entendimiento aprobado | Definidas RN-01 a RN-04 | `Ninguno` |
| `2.1` | Diseño de pantallas | Recorrido de reserva y confirmación | `2. DISEÑO` | `Completada` | `12.0 / 12.0` | `2026-07-12` | `2026-07-12` | Diseño aprobado | Aprobado por el área usuaria | `Ninguno` |
| `2.2` | Modelo de datos | Esquema de salas, franjas y reservas | `2. DISEÑO` | `Bloqueada` | `10.0 / 5.5` | `2026-07-18` | `-` | Modelo de datos | Detenida por credenciales | `STP-01` |
| `3.1` | Servicio de disponibilidad | Consulta de franjas libres por sala (`P-01`, `P-02`) | `3. DESARROLLO` | `No iniciada` | `18.0 / 0.0` | `2026-07-30` | `-` | Servicio en desarrollo | Inicia al liberar el modelo | `STP-01` |
| `3.2` | Registro de reserva | Confirmación, manejo de conflicto y notificación (`P-03`, `P-04`, `P-05`) | `3. DESARROLLO` | `No iniciada` | `10.0 / 0.0` | `2026-08-04` | `-` | Reserva funcional | Depende de `3.1` | `STP-01` |
| `4.1` | Matriz de pruebas | Casos funcionales de RN-01 a RN-04 | `4. QA` | `No iniciada` | `12.0 / 0.0` | `2026-08-06` | `-` | Suite de pruebas | — | `Ninguno` |
| `5.1` | Despliegue | Salida a producción y verificación inicial | `5. PRODUCCIÓN` | `No iniciada` | `10.0 / 0.0` | `2026-08-14` | `-` | Salida a producción | Ventana por acordar | `Ninguno` |

---

## Bitácora del requerimiento

Registro de cada sesión en que el agente actualizó este requerimiento. No es la bitácora de arquitectura de la guía del agente — esa es solo para decisiones de diseño del producto. Esta es el rastro operativo de este requerimiento puntual.

| Fecha | Qué se actualizó | Documentos afectados | Solicitado por |
| :---: | :--- | :--- | :--- |
| `2026-07-06` | Cierre de la fase de requerimiento con RN-01 a RN-04 definidas | [[hu-demo-001-reservar-sala]] | `PO` |
| `2026-07-15` | Registro de `STP-01` por falta de credenciales del ambiente de pruebas | [[seguimiento-demo-req-001]] | `PO` |
| `2026-07-28` | Alta del requerimiento como ejemplo de referencia del repositorio | [[hoja-principal-demo-req-001]], [[seguimiento-demo-req-001]], [[flujo-demo-001-reserva-de-sala]], [[hu-demo-001-reservar-sala]], [[ws-demo-001-consulta-disponibilidad-salas]], [[ws-demo-002-crear-reserva]] | `PO` |
| `2026-07-29` | Alineación de trazabilidad completa (`P-01` a `P-05`, `RN-01` a `RN-04`, tareas EDT `3.1` y `3.2`), sincronización de fechas de corte/actualización y cumplimiento del patrón estrella (DEC-09) | [[hoja-principal-demo-req-001]], [[seguimiento-demo-req-001]], [[flujo-demo-001-reserva-de-sala]], [[hu-demo-001-reservar-sala]], [[ws-demo-001-consulta-disponibilidad-salas]], [[ws-demo-002-crear-reserva]] | `PO` |

**Regla de uso:** una fila por sesión con cambios reales sobre este requerimiento. Una sesión de solo consulta (sin escritura) no genera fila.
