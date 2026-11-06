---
id_documento: PLANTILLA-REQUERIMIENTO-CLIENTE-B1
tipo_documento: plantilla-inmutable
bloque: Bloque 1 - Modelo de requerimiento
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P9
  - P10
  - P11
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-26
estado: Aprobado
---

# Requerimiento del Cliente — Fuente Inmutable [SIGLA]-REQ-[NNN]

Archivo de la solicitud original que dispara toda la documentación del requerimiento.

Este documento tiene una función y solo una: **preservar lo que el cliente pidió, exactamente como lo pidió**. Toda página derivada debe poder rastrearse hasta aquí (P9).


---

## 1. Metadatos de recepción

| Campo | Valor |
| :--- | :--- |
| **ID Requerimiento** | `[SIGLA]-REQ-[NNN]` (ej. `DEMO-REQ-001`) |
| **Título dado por el cliente** | `[Título tal como lo escribió el cliente]` |
| **Fecha de Recepción** | `[AAAA-MM-DD]` |
| **Canal de Recepción** | `[Correo / Formato adjunto / Acta de reunión / Mesa de ayuda]` |
| **Solicitante** | `[Nombre]` |
| **Rol del Solicitante** | `[Cargo]` |
| **Área Solicitante** | `[Área o dependencia]` |
| **Ruta del archivo fuente** | `[Ruta o enlace al archivo original, sin modificar]` |

---

## 2. Solicitud original

> **Regla de inmutabilidad (P9).** Esta sección contiene la transcripción exacta de la solicitud. Queda prohibido editarla, corregir su redacción, resumirla o completarla. Cualquier aclaración posterior del cliente se agrega en la sección 5, nunca aquí.

### 2.1 Datos formales del formato de solicitud

Se completa solo si el cliente usó un formato estructurado. Si envió texto libre, esta subsección se omite.

| Campo del formato | Valor declarado por el cliente |
| :--- | :--- |
| **Sistema o aplicativo** | `[Valor]` |
| **Módulo o funcionalidad** | `[Valor]` |
| **Tipo de requerimiento** | `[Nueva funcionalidad / Mantenimiento / Corrección]` |
| **Objetivo general** | `[Tal como lo escribió el cliente]` |
| **Alcance declarado** | `[Tal como lo redactó el cliente]` |
| **Justificación** | `[Según el cliente]` |
| **Criticidad** | `[Alta / Media / Baja]` |

### 2.2 Transcripción íntegra

```text
[INSERTAR AQUÍ EL TEXTO ÍNTEGRO Y EXACTO ENVIADO POR EL CLIENTE.
No corregir ortografía, no reordenar, no resumir.]
```

### 2.3 Soportes entregados por el cliente

| Archivo o soporte | Formato | Contenido declarado | Ruta |
| :--- | :--- | :--- | :--- |
| `[Nombre del archivo]` | `[Formato]` | `[Para qué lo envió el cliente]` | `[Ruta o enlace]` |

---

## 3. Referencias de consulta provistas

Enlaces o materiales que el cliente entregó como referencia, sin ser parte de la solicitud en sí.

| Tipo de recurso | Propósito | Enlace |
| :--- | :--- | :--- |
| `[Referencia funcional / Módulo existente / Normativa]` | `[Por qué la envió]` | `[Enlace]` |

---

## 4. Interpretación inicial del analista

> **Separación de contexto.** Todo lo que sigue es análisis del equipo, no del cliente. Se mantiene en sección aparte para que nunca se confunda con la fuente. Si el análisis resulta equivocado, esta sección se corrige; la sección 2 no se toca jamás.

### 4.1 Necesidades identificadas

- **Necesidad 1:** `[Síntesis técnica del punto clave]`
- **Necesidad 2:** `[Síntesis técnica del punto clave]`

### 4.2 Trazabilidad hacia el requerimiento

| Elemento | Referencia |
| :--- | :--- |
| **Hoja principal** | `[[plantilla-hoja-principal-requerimiento]]` |
| **Historias de Usuario derivadas** | `[[hu-sigla-nnn-nombre]]` (ver `plantilla-historia-de-usuario`) |
| **Criterio de transformación** | `[Cómo se traduce la solicitud en criterios de aceptación]` |

### 4.3 Vacíos detectados en la solicitud

Lo que el cliente no dijo y hace falta preguntar. Se registra aquí; no se completa por suposición.

| Vacío | A quién se le pregunta | Estado |
| :--- | :--- | :--- |
| `[Qué falta aclarar]` | `[Responsable externo]` | `[Preguntado / Respondido]` |

---

## 5. Historial de aclaraciones del cliente

Si el cliente envía modificaciones o precisiones posteriores, se agregan aquí como bloques nuevos. **Nunca se editan las entradas anteriores ni la sección 2.**

### 5.1 Aclaración del [AAAA-MM-DD]

- **Canal:** `[Correo / Acta]`
- **Texto exacto recibido:**

```text
[Transcripción literal de la aclaración]
```

- **Impacto en la interpretación:** `[Qué cambia en el análisis o en las HU derivadas]`

---

## 6. Ejemplo de referencia

Instancia ficticia y genérica. No corresponde a ningún cliente real.

**Requerimiento:** `DEMO-REQ-001 — Módulo de Reserva de Salas`
**Canal:** Correo electrónico · **Fecha de recepción:** 2026-07-01 · **Solicitante:** Coordinación Administrativa

**Transcripción íntegra:**

```text
"Necesitamos que los empleados puedan reservar las salas de reunión desde la
intranet, viendo cuáles están libres por día y hora. Hoy se hace por correo y
se cruzan reservas. Debería mostrar la capacidad de cada sala y permitir
cancelar con al menos dos horas de anticipación."
```

**Interpretación inicial:**

- **Necesidad 1:** Consulta de disponibilidad por sala, fecha y franja horaria.
- **Necesidad 2:** Registro y cancelación de reservas con regla de anticipación mínima.

**Vacío detectado:** el cliente no indica qué ocurre con reservas recurrentes. Pendiente de preguntar a Coordinación Administrativa.

---

## 7. Reglas de uso

1. **La sección 2 es de solo lectura para siempre.** Ni el agente ni el PO la modifican.
2. **Si el cliente reescribe su solicitud completa,** se agrega como aclaración en la sección 5. No se reemplaza la original.
3. **La interpretación nunca se mezcla con la fuente.** Si una frase no está en el correo del cliente, va en la sección 4.
4. **Las secciones vacías se omiten** (P11).
