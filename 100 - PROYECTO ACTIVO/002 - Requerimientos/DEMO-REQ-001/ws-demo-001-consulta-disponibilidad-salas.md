---
id_documento: WS-DEMO-001
tipo_documento: web-service
id_requerimiento_padre: DEMO-REQ-001
id_canonical: WS-DEMO-001
id_proveedor: "EXT-1001"
nombre_tecnico: "WS_ConsultaDisponibilidadSalas_V1"
alias: ["WS de disponibilidad", "consulta de franjas"]
metodo_http: GET
url_qa: "https://qa.servicios-internos.ejemplo/v1/salas/disponibilidad"
url_prod: "https://api.servicios-internos.ejemplo/v1/salas/disponibilidad"
fuente_verdad: "Inventario interno de espacios"
sla: "2.0s"
estado_definicion: disponible
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-29
---

# Contrato Mínimo de Información de Web Service — WS-DEMO-001

Ficha ficticia de referencia. Las URLs usan el dominio reservado `ejemplo` y no apuntan a ningún servicio real.

**Requerimiento padre:** [[hoja-principal-demo-req-001]] (`DEMO-REQ-001`)

---

## 1. Propósito de Negocio y Justificación

El módulo de reserva no puede ofrecer una franja horaria sin saber si ya está tomada. Este servicio es la única fuente autorizada de disponibilidad: consulta el inventario interno de espacios y devuelve las franjas libres de una sala para una fecha dada. Sin él, la reserva volvería a depender de una hoja de cálculo compartida, que es justamente el problema que el requerimiento resuelve.

* **¿Para qué sirve?:** conocer qué franjas de una sala están libres antes de permitir una reserva.
* **¿Qué hace?:** cruza el inventario de franjas habilitadas de la sala contra las reservas ya confirmadas de esa fecha, y devuelve la diferencia.
* **¿Cómo lo hace?:** consulta de solo lectura sobre el inventario interno de espacios, por identificador de sala y fecha.

---

## 2. Ficha de Especificación Operativa

| Atributo | Especificación |
| :--- | :--- |
| **ID Canónico** | `WS-DEMO-001` |
| **ID Proveedor / Cliente** | `EXT-1001` |
| **Fuente de Verdad** | Inventario interno de espacios |
| **Documento Oficial Proveedor** | No aplica — servicio interno |
| **Protocolo y Encoding** | `REST / JSON (UTF-8)` |
| **Método HTTP** | `GET` |
| **SLA de Rendimiento** | `2.0s` |
| **Llave de Consulta Principal** | `id_sala` + `fecha` |

### 2.1 Autenticación y Headers Obligatorios

| Header | Valor / Formato | Descripción |
| :--- | :--- | :--- |
| `Authorization` | `Bearer [Token]` | Token de sesión del empleado autenticado |
| `Content-Type` | `application/json` | Tipo de contenido esperado en la respuesta |

---

## 3. Estructura de Datos de Entrada (Request)

Parámetros de query. No requiere payload en body.

| Campo (Query) | Tipo de Dato | Obligatoriedad | Descripción / Regla de Formato | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `id_sala` | `String` | `OBLIGATORIO` | Identificador de la sala en el inventario. | `"SALA-A12"` |
| `fecha` | `Date` | `OBLIGATORIO` | Formato `AAAA-MM-DD`. No admite fechas anteriores al día actual. | `"2026-08-03"` |

---

## 4. Estructura de Datos de Salida (Response Exitosa - HTTP 200)

| Campo (JSON) | Tipo de Dato | Obligatoriedad | Descripción | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `codigo_resultado` | `String` | `OBLIGATORIO` | Código funcional (`SUCCESS`, `NOT_FOUND`). | `"SUCCESS"` |
| `id_sala` | `String` | `OBLIGATORIO` | Sala consultada, devuelta como eco de la consulta. | `"SALA-A12"` |
| `capacidad` | `Number` | `OBLIGATORIO` | Capacidad máxima de personas de la sala. | `8` |
| `franjas_libres` | `Array[Object]` | `OBLIGATORIO` | Franjas disponibles. Array vacío si no hay ninguna libre. | `[...]` |

Cada elemento de `franjas_libres` contiene `hora_inicio` y `hora_fin` en formato `HH:MM`.

---

## 5. Matriz de Códigos HTTP y Manejo de Errores

| Código HTTP | Significado Funcional | Causa Raíz / Descripción |
| :---: | :--- | :--- |
| **`200 OK`** | Consulta exitosa | El servicio devolvió las franjas libres de la sala. |
| **`400 Bad Request`** | Error de validación | Falta `id_sala` o `fecha`, o la fecha es anterior al día actual. |
| **`401 Unauthorized`** | Error de autenticación | El token de sesión expiró o es inválido. |
| **`404 Not Found`** | Recurso no encontrado | La sala consultada no existe en el inventario. |
| **`500 Internal Error`** | Error técnico | Fallo interno al consultar el inventario de espacios. |

### 5.1 Ejemplo de Payload de Error Devuelto por el Servicio

```json
{
  "codigo_error": "ERR_SALA_404",
  "mensaje": "La sala SALA-Z99 no existe en el inventario de espacios.",
  "timestamp": "2026-07-28T14:20:00Z"
}
```

---

## 6. Reglas de Desarrollo e Integración (`RN-WS`)

* **`RN-WS-01` (Consulta por llave):** el consumo se ejecuta únicamente enviando la llave combinada `id_sala` + `fecha`.
* **`RN-WS-02` (Políticas de reintento):** ante `HTTP 500` o timeout, el sistema reintenta un máximo de **2 veces con intervalo de 1.0 segundo**.
* **`RN-WS-03` (Manejo de timeout / SLA):** si el servicio supera el SLA de `2.0s` sin responder, se cancela la petición y el módulo aplica el criterio de aceptación `06` de `HU-DEMO-001` — nunca permite confirmar una reserva sin disponibilidad verificada.
