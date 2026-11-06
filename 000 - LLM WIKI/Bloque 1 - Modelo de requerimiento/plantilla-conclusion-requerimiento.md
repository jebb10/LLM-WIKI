---
id_documento: PLANTILLA-CONCLUSION-B1
tipo_documento: plantilla-cierre
bloque: Bloque 1 - Modelo de requerimiento
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-26
estado: Aprobado
---

# Conclusión de Requerimiento — [SIGLA]-REQ-[NNN]

Documento de cierre. Sintetiza lo que el requerimiento entregó, para que un requerimiento cerrado pueda consultarse sin cargar todo su detalle al contexto (P10).

**Tarea de origen:** B1-T08. **Cierra:** DP-15.

---

## 1. Reglas de cierre y reactivación

### 1.1 Cuándo se genera este documento

- **Disparador:** la última tarea de la fase `5. PRODUCCIÓN` pasa a `Completada`.
- **Acción:** el agente compila este documento y actualiza el Estado Macro del requerimiento a `Cerrado en Producción (Dormido)`.
- **Ubicación:** permanece junto al requerimiento. **No se archiva ni se mueve de carpeta**.

### 1.2 Qué significa "dormido"

Ante una consulta general, el agente lee **solo este documento**. El detalle de Historias de Usuario, flujos y contratos técnicos no se carga al contexto salvo solicitud explícita del PO.

Dormir no es ocultar. El requerimiento sigue visible en el índice, en una sola línea, con enlace a esta conclusión.

### 1.3 Qué ocurre cuando llega soporte

Regla única. Cuando el cliente reporta una necesidad sobre un requerimiento cerrado:

| Paso | Documento | Qué se hace |
| :---: | :--- | :--- |
| 1 | `plantilla-seguimiento-requerimiento.md` | Se agregan las tareas de soporte, con su fase. El Estado Macro vuelve a derivarse de las fases. |
| 2 | Historia de Usuario afectada | Se **actualiza directamente**. La HU es la referencia vigente para mantenimiento. |
| 3 | `plantilla-requerimiento-cliente.md` | La nueva solicitud se registra como aclaración en su historial (sección 5). |
| 4 | **Este documento** | Se agrega **una fila** en la sección 8. No se reescribe, no se re-versiona, no se duplica. |

**Regla de no destrucción:** las secciones 2 a 7 de este documento reflejan el cierre original y no se modifican por una actividad de soporte. Al terminar el soporte, se actualizan únicamente los datos de horas de la sección 5 y se cierra la fila abierta en la sección 8.

---

## 2. Metadatos de cierre

| Campo | Valor |
| :--- | :--- |
| **ID Requerimiento** | `[SIGLA]-REQ-[NNN]` (ej. `DEMO-REQ-001`) |
| **Título** | `[Nombre completo]` |
| **Fecha de Cierre** | `[AAAA-MM-DD]` |
| **Responsable** | `[Nombre del PO]` |
| **Acta de entrega** | `[Pendiente / Firmada el AAAA-MM-DD — ruta]` |
| **Estado Macro** | `Cerrado en Producción (Dormido)` |

---

## 3. Resumen ejecutivo final

`[Dos o tres líneas. Qué quedó en producción y qué valor entregó. Debe bastar para responder por este requerimiento sin abrir nada más.]`

- **Objetivo logrado:** `[Funcionalidad desplegada]`
- **Componentes impactados:** `[Sistemas o módulos modificados]`

---

## 4. Alcance final entregado

> Los Web Services se referencian siempre por su ID canónico (`REGLA-IDENTIFICADOR-WS.md`), nunca por nombre informal ni por posición en el flujo.

| Historia de Usuario | Título | Servicios asociados | Estado |
| :--- | :--- | :--- | :---: |
| `HU-[SIGLA]-[NNN]` | `[Título]` | `[IDs canónicos de los servicios]` | `En producción` |

**Fuera de alcance final:** `[Lo que se pidió y no se entregó, con la razón. Si no hubo, se omite esta línea.]`

---

## 5. Estado final de horas

Corte consolidado. El detalle contable permanece en el Excel (P7).

| Métrica | Estimado | Ejecutado | Desviación |
| :--- | :---: | :---: | :---: |
| **Horas totales** | `0.0 hrs` | `0.0 hrs` | `0.0 hrs` |
| **Fecha de cierre** | `[AAAA-MM-DD]` | `[AAAA-MM-DD]` | `0 días` |

---

## 6. Decisiones clave

Decisiones tomadas durante la ejecución que condicionan cómo se comporta hoy el sistema. Se extraen del log del requerimiento.

| Decisión | Qué se resolvió | Fecha |
| :--- | :--- | :---: |
| `[DEC-XX]` | `[Resumen en una línea]` | `[AAAA-MM-DD]` |

---

## 7. Lecciones aprendidas y deuda heredada

### 7.1 Lecciones

- `[Aprendizaje aplicable a futuros requerimientos]`

### 7.2 Deuda técnica

| ID | Componente | Descripción | Criticidad |
| :---: | :--- | :--- | :---: |
| `[DEU-01]` | `[Componente]` | `[Ajuste diferido]` | `[Criticidad]` |

---

## 8. Historial de soporte post-cierre

Se agrega una fila por cada actividad de soporte. Ninguna fila se borra ni se edita al cerrarse: se actualiza su estado.

| Fecha | Solicitud | Motivo | Documentos actualizados | Estado |
| :---: | :--- | :--- | :--- | :---: |
| `[AAAA-MM-DD]` | `[SOP-XXX]` | `[Qué pidió el cliente]` | `[HU-XX, seguimiento]` | `[Abierta / Cerrada]` |

---

## 9. Reglas de uso

1. **Este documento no reemplaza al centralizador.** Es su síntesis; el detalle de tareas permanece en el documento de seguimiento.
2. **Un requerimiento cerrado no se archiva.** Se duerme
3. **El soporte agrega, no reescribe.** Una fila en la sección 8, nunca un documento nuevo (P11).
4. **Las secciones vacías se omiten.**
