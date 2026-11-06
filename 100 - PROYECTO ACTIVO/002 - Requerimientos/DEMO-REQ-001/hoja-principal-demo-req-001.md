---
id_documento: DEMO-REQ-001
tipo_documento: requerimiento
sigla_modulo: DEMO
naturaleza: Desarrollo
sponsor_po: Nombre del PO
estado_macro: Bloqueado
fecha_recepcion: 2026-07-01
fecha_actualizacion: 2026-07-29
estado: Aprobado
---

# Hoja Principal del Requerimiento — DEMO-REQ-001

Página raíz del requerimiento. Permite entender **qué es** y **en qué va** el requerimiento sin abrir ningún otro documento (P10).

> **Ejemplo de referencia del repositorio.** Requerimiento ficticio y genérico, sin relación con ningún cliente real. Existe para mostrar el modelo instanciado de punta a punta; se elimina al arrancar un proyecto propio (ver el Checklist de Arranque de Proyecto Nuevo en la guía del agente).

---

## 1. Resumen ejecutivo

Módulo web para que los empleados reserven salas de reuniones consultando disponibilidad real, evitando cruces de horario entre equipos. El diseño funcional está aprobado y el desarrollo está detenido: falta habilitar el ambiente de pruebas para cerrar el modelo de datos de disponibilidad.

| Campo | Valor |
| :--- | :--- |
| **ID** | `DEMO-REQ-001` |
| **Título** | Módulo de Reserva de Salas |
| **Naturaleza** | Desarrollo |
| **Fecha de Recepción** | `2026-07-01` |
| **Sponsor / PO** | Nombre del PO |
| **Analista** | Nombre del analista |
| **Estado Macro** | `Bloqueado` (derivado — fase 2 en estado `Bloqueada`) |
| **Avance** | `37 %` al corte del `2026-07-25` |

---

## 2. Contexto

Las salas de reuniones se reservaban por mensajes informales y una hoja de cálculo compartida, sin validación de cruces. El resultado eran reuniones desplazadas y salas ocupadas por equipos que no las habían reservado. El área usuaria solicitó un módulo con disponibilidad consultable y confirmación registrada, como único mecanismo válido de reserva.

---

## 3. Actores y stakeholders

| Rol / Actor | Descripción | Responsabilidad en el flujo |
| :--- | :--- | :--- |
| Empleado registrado | Colaborador con cuenta activa en el directorio interno | Consulta disponibilidad y confirma la reserva |
| Administrador de espacios | Responsable de la operación de las salas | Define el inventario de salas y sus franjas habilitadas |

---

## 4. Reglas de negocio macro

| ID | Regla | Origen |
| :---: | :--- | :--- |
| `RN-01` | No se admite una reserva con menos de dos horas de anticipación respecto a la hora de inicio. | Solicitud del área usuaria |
| `RN-02` | Una franja horaria de una sala admite una sola reserva confirmada. | Solicitud del área usuaria |
| `RN-03` | Solo un empleado con cuenta activa en el directorio interno puede confirmar una reserva. | Política interna de accesos |
| `RN-04` | La duración mínima de una reserva es de 30 minutos y la máxima de 4 horas continuas. | Solicitud del área usuaria |

Las reglas de detalle de cada funcionalidad viven en su Historia de Usuario.

---

## 5. Integraciones

| Web Service | Para qué se usa | Estado |
| :--- | :--- | :--- |
| `WS-DEMO-001` | Consulta de franjas libres por sala y fecha | `disponible` |
| `WS-DEMO-002` | Registro de la reserva confirmada | `en-contrato` |

**Prohibido:** referenciar un servicio por su posición en el flujo (`WS 4`, `el segundo servicio`) o por URL. Esa práctica es la brecha que el producto existe para cerrar.

---

## 6. Flujo funcional

- **Flujo principal:** [[flujo-demo-001-reserva-de-sala]]
- **Mockups:** No aplica.

---

## 7. Estimación y estado

- **Documento centralizador de seguimiento:** [[seguimiento-demo-req-001]]
- **Horas estimadas totales:** `86.0 hrs`
- **Horas consumidas al corte:** `31.5 hrs` (corte `2026-07-25`)
- **Stoppers activos:** `1` — el detalle se consulta en el documento centralizador.

No se repite aquí la tabla de tareas ni la de stoppers. Duplicarlas rompe la propagación: el mismo dato quedaría en dos lugares y solo uno se actualizaría.

---

## 8. Pendientes de decisión externa

| Qué falta definir | Quién debe definirlo | Desde cuándo | Impacto si no llega |
| :--- | :--- | :---: | :--- |
| Credenciales del ambiente de pruebas | Área de Infraestructura | `2026-07-15` | Bloquea el modelo de datos y, en cascada, el desarrollo del servicio de disponibilidad |

---

## 9. Enlaces del requerimiento

| Documento | Enlace |
| :--- | :--- |
| Documento centralizador de seguimiento | [[seguimiento-demo-req-001]] |
| Historias de Usuario | [[hu-demo-001-reservar-sala]] |
| Flujos funcionales | [[flujo-demo-001-reserva-de-sala]] |
| Web Services | [[ws-demo-001-consulta-disponibilidad-salas]] · [[ws-demo-002-crear-reserva]] |
| Tabla de trazabilidad | Vive en el documento centralizador de seguimiento (§ Tabla de trazabilidad) |
| Tablero consolidado del proyecto | [[000 - Plan de Trabajo - Cronograma de Requerimientos]] |

Sin solicitud original de cliente: este requerimiento de ejemplo no tiene `_fuente-cliente/`, y esa carpeta es opcional.
