---
id_documento: WS-DEMO-002
tipo_documento: web-service
id_requerimiento_padre: DEMO-REQ-001
id_canonical: WS-DEMO-002
id_proveedor: "EXT-1002"
nombre_tecnico: "WS_CrearReservaSala_V1"
alias: ["WS de reserva", "registro de reserva"]
metodo_http: POST
url_qa: "https://qa.servicios-internos.ejemplo/v1/salas/reservas"
url_prod: "https://api.servicios-internos.ejemplo/v1/salas/reservas"
fuente_verdad: "Inventario interno de espacios"
sla: "3.0s"
estado_definicion: en-contrato
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-29
---

# Contrato Mínimo de Información de Web Service — WS-DEMO-002

Ficha ficticia de referencia. Las URLs usan el dominio reservado `ejemplo` y no apuntan a ningún servicio real.

**Requerimiento padre:** [[hoja-principal-demo-req-001]] (`DEMO-REQ-001`)

Su `estado_definicion` es `en-contrato`: el contrato está acordado pero el endpoint aún no está habilitado en el ambiente de pruebas — es el mismo bloqueo que registra `STP-01` en el documento de Seguimiento.

---

## 1. Propósito de Negocio y Justificación

Consultar disponibilidad no reserva nada. Este servicio es el que convierte una intención en una reserva real: registra la franja a nombre del empleado y la vuelve indisponible para el resto. Es el único punto donde se materializa la regla de una sola reserva confirmada por franja, y por eso la validación de conflicto vive del lado del servicio y no solo de la interfaz.

* **¿Para qué sirve?:** registrar de forma definitiva la reserva de una franja de sala.
* **¿Qué hace?:** valida que la franja siga libre, valida la anticipación mínima, y persiste la reserva devolviendo su identificador.
* **¿Cómo lo hace?:** escritura transaccional sobre el inventario interno de espacios, rechazando la operación si otra reserva ganó la misma franja entre la consulta y la confirmación.

---

## 2. Ficha de Especificación Operativa

| Atributo | Especificación |
| :--- | :--- |
| **ID Canónico** | `WS-DEMO-002` |
| **ID Proveedor / Cliente** | `EXT-1002` |
| **Fuente de Verdad** | Inventario interno de espacios |
| **Documento Oficial Proveedor** | No aplica — servicio interno |
| **Protocolo y Encoding** | `REST / JSON (UTF-8)` |
| **Método HTTP** | `POST` |
| **SLA de Rendimiento** | `3.0s` |
| **Llave de Consulta Principal** | `id_sala` + `fecha` + `hora_inicio` |

### 2.1 Autenticación y Headers Obligatorios

| Header | Valor / Formato | Descripción |
| :--- | :--- | :--- |
| `Authorization` | `Bearer [Token]` | Token de sesión del empleado autenticado |
| `Content-Type` | `application/json` | Tipo de contenido enviado en el body |

---

## 3. Estructura de Datos de Entrada (Request)

| Campo (JSON) | Tipo de Dato | Obligatoriedad | Descripción / Regla de Formato | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `id_sala` | `String` | `OBLIGATORIO` | Identificador de la sala en el inventario. | `"SALA-A12"` |
| `fecha` | `Date` | `OBLIGATORIO` | Formato `AAAA-MM-DD`. | `"2026-08-03"` |
| `hora_inicio` | `String` | `OBLIGATORIO` | Formato `HH:MM`, en franjas de 30 minutos. | `"09:30"` |
| `duracion_minutos` | `Number` | `OBLIGATORIO` | Entre 30 y 240, en múltiplos de 30. | `60` |
| `motivo` | `String` | `OPCIONAL` | Máximo 140 caracteres. | `"Comité de seguimiento"` |

---

## 4. Estructura de Datos de Salida (Response Exitosa - HTTP 201)

| Campo (JSON) | Tipo de Dato | Obligatoriedad | Descripción | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `codigo_resultado` | `String` | `OBLIGATORIO` | Código funcional (`CREATED`, `CONFLICT`). | `"CREATED"` |
| `id_reserva` | `String` | `OBLIGATORIO` | Identificador de la reserva registrada. | `"RES-2026-004512"` |
| `estado_reserva` | `String` | `OBLIGATORIO` | Estado de la reserva (`CONFIRMADA`, `RECHAZADA`). | `"CONFIRMADA"` |
| `notificacion_enviada` | `Boolean` | `OBLIGATORIO` | Indica si se notificó al solicitante. | `true` |

---

## 5. Matriz de Códigos HTTP y Manejo de Errores

| Código HTTP | Significado Funcional | Causa Raíz / Descripción |
| :---: | :--- | :--- |
| **`201 Created`** | Reserva registrada | La franja estaba libre y la reserva quedó confirmada. |
| **`400 Bad Request`** | Error de validación | Falta un campo obligatorio, o la duración está fuera del rango permitido. |
| **`401 Unauthorized`** | Error de autenticación | El token de sesión expiró o es inválido. |
| **`403 Forbidden`** | Cuenta no habilitada | La cuenta del empleado está inactiva en el directorio interno (`RN-03`). |
| **`409 Conflict`** | Franja ya reservada | Otra reserva confirmada ocupó la franja antes de esta petición (`RN-02`). |
| **`422 Unprocessable`** | Anticipación insuficiente | Falta menos de dos horas para el inicio de la franja (`RN-01`). |
| **`500 Internal Error`** | Error técnico | Fallo interno al persistir la reserva. |

### 5.1 Ejemplo de Payload de Error Devuelto por el Servicio

```json
{
  "codigo_error": "ERR_FRANJA_409",
  "mensaje": "La franja 09:30 de la sala SALA-A12 ya tiene una reserva confirmada.",
  "timestamp": "2026-07-28T14:22:00Z"
}
```

---

## 6. Reglas de Desarrollo e Integración (`RN-WS`)

* **`RN-WS-01` (Validación en servidor):** la validación de conflicto de franja y de anticipación mínima se ejecuta siempre del lado del servicio, incluso si la interfaz ya la validó. La interfaz no es fuente de verdad.
* **`RN-WS-02` (Sin reintento automático en conflicto):** ante `HTTP 409` o `HTTP 422` el sistema **no** reintenta — devuelve el conflicto al empleado. El reintento (máximo 2 veces, intervalo de 1.0 segundo) aplica únicamente ante `HTTP 500` o timeout.
* **`RN-WS-03` (Idempotencia):** dos peticiones idénticas consecutivas no generan dos reservas; la segunda recibe `HTTP 409`.
