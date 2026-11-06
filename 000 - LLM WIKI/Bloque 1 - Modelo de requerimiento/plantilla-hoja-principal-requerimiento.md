---
id_documento: PLANTILLA-HOJA-PRINCIPAL-B1
tipo_documento: plantilla
bloque: Bloque 1 - Modelo de requerimiento
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P10
  - P11
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-27
estado: Aprobado
---

# Hoja Principal del Requerimiento — [SIGLA]-REQ-[NNN]

Página raíz del requerimiento. Funciona como README: permite entender **qué es** y **en qué va** el requerimiento sin abrir ningún otro documento (P10).

No contiene tareas ni stoppers: esos viven en el documento centralizador de seguimiento y se consultan allí.

**Tarea de origen:** B1-T06.

---

## 1. Resumen ejecutivo

`[Dos o tres líneas. Qué resuelve el requerimiento y en qué estado se encuentra. Esta sección debe bastar para responder por el requerimiento sin leer el resto de la página.]`

| Campo | Valor |
| :--- | :--- |
| **ID** | `[SIGLA]-REQ-[NNN]` (ej. `DEMO-REQ-001`) |
| **Título** | `[Nombre del requerimiento]` |
| **Naturaleza** | `[Desarrollo / Soporte]` |
| **Fecha de Recepción** | `[AAAA-MM-DD]` |
| **Sponsor / PO** | `[Nombre]` |
| **Analista** | `[Nombre]` |
| **Estado Macro** | `[Derivado — ver MODELO-REQUERIMIENTO.md §1.3]` |
| **Avance** | `[N %]` al corte del `[AAAA-MM-DD]` |

---

## 2. Contexto

`[Por qué existe este requerimiento. Antecedente de negocio u operativo que lo origina. Prosa breve, no lista de tareas.]`

---

## 3. Actores y stakeholders

Los actores viven aquí. No se crean páginas independientes de Actor.

| Rol / Actor | Descripción | Responsabilidad en el flujo |
| :--- | :--- | :--- |
| `[Rol]` | `[Quién es]` | `[Qué hace o qué decide]` |

---

## 4. Reglas de negocio macro

Las reglas macro viven aquí. No se crean páginas independientes de Regla de Negocio (DEC-09).

Las reglas de detalle de cada funcionalidad viven en su Historia de Usuario.

| ID | Regla | Origen |
| :---: | :--- | :--- |
| `RN-01` | `[Enunciado de la regla]` | `[Solicitud del cliente / decisión / normativa]` |

---

## 5. Integraciones

Cada Web Service se documenta con su ficha propia (`plantilla-contrato-ws.md`) y se enlaza aquí solo por su ID canónico (`ONTOLOGIA.md` §5.4).

| Web Service | Para qué se usa | Estado |
| :--- | :--- | :--- |
| `[[ws-sigla-nnn-nombre]]` | `[Propósito funcional en una línea]` | `pendiente-proveedor / en-contrato / disponible / deprecado` |

**Prohibido:** referenciar un servicio por su posición en el flujo (`WS 4`, `el quinto servicio`) o por URL. Esa práctica es la brecha que el producto existe para cerrar.

---

## 6. Flujo funcional

El flujo detallado (diagrama Mermaid y tabla de pasos) vive en su propio documento (`plantilla-flujo-funcional.md`). Esta sección solo enlaza, no transcribe.

- **Flujo principal:** `[[nombre-del-documento-de-flujo]]`
- **Mockups:** `[Enlace o "No aplica"]`

---

## 7. Estimación y estado

- **Documento centralizador de seguimiento:** `[[plantilla-seguimiento-requerimiento]]`
- **Horas estimadas totales:** `[N] hrs`
- **Horas consumidas al corte:** `[N] hrs` (corte `[AAAA-MM-DD]`)
- **Stoppers activos:** `[N]` — el detalle se consulta en el documento centralizador.

No se repite aquí la tabla de tareas ni la de stoppers. Duplicarlas rompe la propagación: el mismo dato quedaría en dos lugares y solo uno se actualizaría.

---

## 8. Pendientes de decisión externa

Lo que este requerimiento necesita de terceros para poder avanzar. Cada línea debe tener responsable.

| Qué falta definir | Quién debe definirlo | Desde cuándo | Impacto si no llega |
| :--- | :--- | :---: | :--- |
| `[Definición pendiente]` | `[Área, proveedor o persona]` | `[AAAA-MM-DD]` | `[Consecuencia]` |

---

## 9. Enlaces del requerimiento

| Documento | Enlace |
| :--- | :--- |
| Solicitud original del cliente (inmutable) | `[[plantilla-requerimiento-cliente]]` |
| Documento centralizador de seguimiento | `[[plantilla-seguimiento-requerimiento]]` |
| Historias de Usuario | `[[hu-sigla-nnn-nombre]]` (una por HU, ver `plantilla-historia-de-usuario`) |
| Flujos funcionales | `[[nombre-del-documento-de-flujo]]` (ver `plantilla-flujo-funcional`) |
| Web Services | `[[ws-sigla-nnn-nombre]]` (una por endpoint, ver `plantilla-contrato-ws`) |
| Tabla de trazabilidad | Vive en el documento centralizador de seguimiento (§ Tabla de trazabilidad) |
| Conclusión (solo al cerrar) | `[[plantilla-conclusion-requerimiento]]` |

---

## 10. Reglas de uso

1. **El resumen ejecutivo se actualiza en cada cambio de estado.** Si queda viejo, esta página deja de cumplir su función.
2. **Las secciones vacías se omiten.** No se dejan tablas con marcadores sin llenar (P11).
3. **Esta página enlaza, no repite.** Cualquier dato que ya viva en otro documento se referencia.
4. **Las secciones 5 y 6 solo enlazan documentos de Bloque 2** (`plantilla-contrato-ws.md`, `plantilla-flujo-funcional.md`). Nunca transcriben su contenido.
