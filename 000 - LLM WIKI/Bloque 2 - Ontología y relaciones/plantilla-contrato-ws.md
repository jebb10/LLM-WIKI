---
id_documento: PLANTILLA-CONTRATO-WS-B2
tipo_documento: plantilla
bloque: Bloque 2 - Ontología y relaciones
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P10
  - P11
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-27
estado: Aprobado
---

# Contrato Mínimo de Información de Web Service — [WS-SIGLA-NNN]

Plantilla y norma técnica de integración. Define la estructura obligatoria que debe contener toda ficha de Web Service en la wiki para garantizar que sea un **recurso enriquecido**: que explique por qué está el servicio allí, para qué sirve, qué hace, cómo lo hace y el detalle técnico principal.

* **Autor:** Johan Benítez — Product Owner / Líder de Requerimientos
* **Tarea de origen:** `B2-T04` (Bloque 2 — Ontología y relaciones)
* **Definición que cierra:** `DP-01` (Contrato mínimo de información de un Web Service)
* **Estado:** Aprobado

---

## Metadatos Estándar (YAML Frontmatter)

Toda ficha de Web Service debe iniciar obligatoriamente en la línea 1 con la siguiente cabecera:

```yaml
---
id_canonical: WS-[SIGLA]-[NNN]
id_proveedor: "[ID dado por el cliente/proveedor — ej. EXT-1234]"
nombre_tecnico: "[Nombre_Tecnico_del_Endpoint]"
alias: ["WS N", "Nombre informal 1", "Nombre informal 2"]
metodo_http: GET | POST | PUT | PATCH | DELETE
url_qa: "https://qa.proveedor.com/v1/endpoint"
url_prod: "https://api.proveedor.com/v1/endpoint"
fuente_verdad: "[Sistema dueño del dato — ej. Core del proveedor externo]"
documento_proveedor: "[[enlace-o-referencia-al-documento-tecnico-oficial-del-proveedor]]"
estado_definicion: pendiente-proveedor | en-contrato | disponible | deprecado
---
```

**Granularidad (cierra B2-T05):** una ficha por endpoint. Un endpoint reutilizado por varias HU/pasos del mismo requerimiento se referencia desde una sola ficha; entre requerimientos distintos sí se duplica (ver `ONTOLOGIA.md` §5.5).

---

## 1. Propósito de Negocio y Justificación

`[Dos o tres párrafos en prosa clara. Esta sección responde a la pregunta de negocio: ¿Por qué existe este Web Service en el proyecto? ¿Qué valor aporta? ¿Qué problema resuelve para el usuario o el proceso?]`

* **¿Para qué sirve?:** `[Descripción breve de la utilidad del servicio.]`
* **¿Qué hace?:** `[Explicación del procesamiento o cálculo funcional que ejecuta.]`
* **¿Cómo lo hace?:** `[Resumen del flujo técnico de consulta e integración.]`

---

## 2. Ficha de Especificación Operativa

| Atributo | Especificación |
| :--- | :--- |
| **ID Canónico** | `WS-[SIGLA]-[NNN]` (ej. `WS-DEMO-001`) |
| **ID Proveedor / Cliente** | `[ID externo — ej. EXT-1234]` *(Cierra DP-27)* |
| **Fuente de Verdad** | `[Sistema dueño del dato — ej. Core del proveedor externo]` |
| **Documento Oficial Proveedor** | `[Referencia o enlace al PDF/Swagger/Doc entregado por el proveedor]` |
| **Protocolo y Encoding** | `REST / JSON (UTF-8)` |
| **Método HTTP** | `[GET / POST / PUT / PATCH / DELETE]` |
| **SLA de Rendimiento** | `[SLA tolerado en segundos — ej. 3.0s (si aplica)]` |
| **Llave de Consulta Principal** | `[Campos que identifican la búsqueda — ej. tipo_documento + numero_documento]` |

### 2.1 Autenticación y Headers Obligatorios

| Header | Valor / Formato | Descripción |
| :--- | :--- | :--- |
| `Authorization` | `Bearer [Token]` | Token de autenticación de sesión |
| `Content-Type` | `application/json` | Tipo de contenido enviado |
| `X-Api-Key` | `[API-Key-Cliente]` | Clave de acceso concedida por el proveedor |

---

## 3. Estructura de Datos de Entrada (Request)

`[Aplica cuando el servicio recibe payload en body o parámetros en query/path. Si es un GET sin parámetros, indicar: "No requiere payload de entrada."]`

| Campo (JSON / Query) | Tipo de Dato | Obligatoriedad | Descripción / Regla de Formato | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `tipo_documento` | `String` | `OBLIGATORIO` | Tipo de documento de identidad (`CC`, `CE`, `PAS`). | `"CC"` |
| `numero_documento` | `String` | `OBLIGATORIO` | Número de documento sin puntos ni guiones. | `"1018456789"` |
| `fecha_nacimiento` | `Date` | `CONDICIONADO` | Formato `AAAA-MM-DD`. Obligatorio si tipo es `CC`. | `"1990-05-15"` |
| `email_contacto` | `String` | `OPCIONAL` | Correo electrónico válido de notificación. | `"usuario@correo.com"` |

* **Niveles de Obligatoriedad Permitidos:** `OBLIGATORIO` | `OPCIONAL` | `CONDICIONADO` *(explicar la condición que lo activa en la descripción)*.

---

## 4. Estructura de Datos de Salida (Response Exitosa - HTTP 200/201)

| Campo (JSON) | Tipo de Dato | Obligatoriedad | Descripción | Ejemplo |
| :--- | :---: | :---: | :--- | :--- |
| `codigo_resultado` | `String` | `OBLIGATORIO` | Código de respuesta funcional (`SUCCESS`, `NOT_FOUND`). | `"SUCCESS"` |
| `estado_afiliado` | `String` | `OBLIGATORIO` | Estado del asegurado en el sistema (`ACTIVO`, `INACTIVO`). | `"ACTIVO"` |
| `nombre_completo` | `String` | `OBLIGATORIO` | Nombres y apellidos concatenados. | `"PÉREZ GÓMEZ JUAN"` |
| `productos` | `Array[Object]` | `CONDICIONADO` | Lista de pólizas. Devuelto solo si `estado_afiliado == ACTIVO`. | `[...]` |

---

## 5. Matriz de Códigos HTTP y Manejo de Errores

| Código HTTP | Significado Funcional | Causa Raíz / Descripción |
| :---: | :--- | :--- |
| **`200 OK`** | Consulta Exitosa | El servicio procesó la consulta y devolvió los datos requeridos. |
| **`400 Bad Request`** | Error de Validación | Algún campo obligatorio falta o no cumple el formato esperado. |
| **`401 Unauthorized`** | Error de Autenticación | El token o API Key expiró o es inválido. |
| **`404 Not Found`** | Recurso no Encontrado | El documento consultado no existe en la fuente de verdad. |
| **`500 Internal Error`** | Error Técnico del Proveedor | Fallo interno en la infraestructura del proveedor (ej. base de datos caída). |

### 5.1 Ejemplo de Payload de Error Devuelto por el Servicio

```json
{
  "codigo_error": "ERR_EXT_404",
  "mensaje": "El número de documento 1018456789 no se encuentra registrado en el sistema externo.",
  "timestamp": "2026-07-26T16:50:00Z"
}
```

---

## 6. Reglas de Desarrollo e Integración (`RN-WS`)

Reglas técnicas de negocio dirigidas al desarrollador para el consumo del servicio:

* **`RN-WS-01` (Consulta por Llave):** El consumo debe ejecutarse únicamente enviando la llave combinada `tipo_documento` + `numero_documento`.
* **`RN-WS-02` (Políticas de Reintento):** Ante una respuesta `HTTP 500` o `Timeout`, el sistema reintentará el consumo un máximo de **3 veces con intervalo de 1.0 segundo**.
* **`RN-WS-03` (Manejo de Timeout / SLA):** Si el servicio supera el SLA de `3.0s` sin responder, se cancela la petición y se registra un evento de advertencia, derivando en un `Stopper` si impide la continuidad del flujo.
