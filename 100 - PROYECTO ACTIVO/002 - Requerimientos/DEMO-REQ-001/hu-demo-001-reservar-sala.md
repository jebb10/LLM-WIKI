---
id_documento: HU-DEMO-001
tipo_documento: historia-usuario
id_requerimiento_padre: DEMO-REQ-001
paso_flujo_id: P-01, P-03, P-04, P-05
actor: Empleado registrado
fecha_creacion: 2026-07-06
fecha_actualizacion: 2026-07-29
estado: Aprobado
---

# Historia de Usuario — HU-DEMO-001

---

## 1. Identificación de la Historia de Usuario

| Campo | Valor |
| :--- | :--- |
| **Id. Historia de Usuario** | `HU-DEMO-001` |
| **Nombre** | Reservar sala de reuniones |
| **Requerimiento padre** | [[hoja-principal-demo-req-001]] (`DEMO-REQ-001`) |
| **Paso de Flujo** | `P-01`, `P-03`, `P-04`, `P-05` — ver `flujo-demo-001-reserva-de-sala` |
| **Épica / Feature** | Épica: Gestión de espacios / Feature: Reserva de salas |
| **Actor** | Empleado registrado |
| **Prioridad** | `Alta` |
| **Dependencias HU** | Ninguna |
| **Pre-condiciones** | El inventario de salas y sus franjas habilitadas debe estar cargado por el Administrador de espacios. |

---

## 2. Escenario de la HU

| Pregunta clave | Contenido |
| :--- | :--- |
| **Como** (rol) | Empleado registrado |
| **Quiero** (objetivo) | Reservar una sala de reuniones disponible |
| **Para** (beneficio) | Coordinar reuniones sin cruzar horarios con otro equipo |

---

## 3. Reglas de negocio

| ID | Descripción |
| :---: | :--- |
| `RN-01` | No se admite una reserva con menos de dos horas de anticipación respecto a la hora de inicio. |
| `RN-02` | Una franja horaria de una sala admite una sola reserva confirmada. |
| `RN-03` | Solo un empleado con cuenta activa en el directorio interno puede confirmar una reserva. |
| `RN-04` | La duración mínima de una reserva es de 30 minutos y la máxima de 4 horas continuas. |

---

## 4. Criterios de aceptación

| No. | Dado que | Cuando | Entonces |
| :---: | :--- | :--- | :--- |
| `01` | La sala está libre en el horario elegido y falta más de dos horas para el inicio | Confirmo la reserva | El sistema la registra y notifica al solicitante |
| `02` | La sala ya tiene una reserva confirmada en ese horario | Intento confirmar | El sistema rechaza la reserva y muestra el conflicto de horario |
| `03` | Falta menos de dos horas para el inicio del horario elegido | Intento confirmar | El sistema rechaza la reserva indicando la anticipación mínima exigida |
| `04` | Mi cuenta del directorio interno está inactiva | Intento confirmar | El sistema rechaza la operación y no registra ninguna reserva |
| `05` | Elijo una duración mayor a 4 horas continuas | Intento confirmar | El sistema rechaza la reserva indicando la duración máxima permitida |
| `06` | El servicio de disponibilidad no responde dentro de su SLA | Consulto disponibilidad | El sistema informa que la disponibilidad no pudo verificarse y no permite confirmar a ciegas |

Los criterios cubren happy path (`01`), unhappy path (`02` a `05`) y escenario alterno de falla técnica (`06`).

---

## 5. Prototipos / Mockup

No aplica. Los prototipos son orientativos, no contractuales.

---

## 6. Flujo

- **Flujo:** `flujo-demo-001-reserva-de-sala`
- **Paso de esta HU dentro del flujo:** `P-01` (consulta), `P-03` (confirmación), `P-04` (conflicto de horario) y `P-05` (notificación)

---

## 7. Web Service asociado

| Web Service | Rol en este paso |
| :--- | :--- |
| `WS-DEMO-001` | Consulta las franjas libres de una sala en la fecha elegida |
| `WS-DEMO-002` | Registra la reserva confirmada sobre la franja seleccionada |

Solo se referencia el ID canónico del servicio. El detalle técnico vive únicamente en la ficha del WS.

---

## 8. Datos de entrada (input) y datos de salida (output)

| Campo | Dirección | Tipo (genérico) | Obligatoriedad | Longitud | Detalle |
| :--- | :---: | :---: | :---: | :--- | :--- |
| `id_sala` | Entrada (`P-01`, `P-03`) | `Texto` | `Obligatorio` | Máx. 12 caracteres | Identificador de la sala del inventario |
| `fecha` | Entrada (`P-01`, `P-03`) | `Fecha` | `Obligatorio` | 10 caracteres | Formato `AAAA-MM-DD`, nunca anterior al día actual |
| `hora_inicio` | Entrada (`P-03`) | `Texto` | `Obligatorio` | 5 caracteres | Formato `HH:MM` en franjas de 30 minutos |
| `duracion_minutos` | Entrada (`P-03`) | `Numérico` | `Obligatorio` | Máx. 3 dígitos | Entre 30 y 240, en múltiplos de 30 |
| `motivo` | Entrada (`P-03`) | `Texto` | `Opcional` | Máx. 140 caracteres | Descripción breve visible para el Administrador de espacios |
| `capacidad` | Salida (`P-01`) | `Numérico` | `Obligatorio` | Máx. 3 dígitos | Capacidad máxima de personas de la sala consultada |
| `franjas_libres` | Salida (`P-01`) | `Lista` | `Obligatorio` | — | Lista de bloques disponibles con `hora_inicio` y `hora_fin` (`HH:MM`) |
| `id_reserva` | Salida (`P-03`, `P-05`) | `Texto` | `Obligatorio` | Máx. 20 caracteres | Código único de confirmación (ej. `RES-2026-004512`) mostrado y enviado al solicitante |
| `estado_reserva` | Salida (`P-03`, `P-04`) | `Texto` | `Obligatorio` | — | Estado resultante (`CONFIRMADA` o `RECHAZADA` con mensaje de conflicto/validación) |
| `notificacion_enviada` | Salida (`P-05`) | `Booleano` | `Obligatorio` | — | Confirmación de envío del comprobante al correo institucional del empleado registrado |

---

## 9. Notas

Requerimiento no funcional: la consulta de disponibilidad debe responder dentro del SLA declarado en la ficha de `WS-DEMO-001`; si lo supera, el criterio de aceptación `06` define el comportamiento esperado.

---

## 11. Aprobadores

| Versión | Fecha | Autor | Revisado por | Aprobado por | Rol del aprobador | Descripción de cambio | Estado |
| :---: | :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| `V1` | `2026-07-06` | | | | | | `Pendiente` |

Los campos de control quedan vacíos para llenado manual; el agente no los completa por su cuenta.
