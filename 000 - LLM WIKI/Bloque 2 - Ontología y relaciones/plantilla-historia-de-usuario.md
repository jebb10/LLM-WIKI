---
id_documento: PLANTILLA-HISTORIA-USUARIO-B2
tipo_documento: plantilla
bloque: Bloque 2 - Ontología y relaciones
principios_aplicados:
  - P1
  - P2
  - P4
  - P6
  - P8
  - P9
  - P10
  - P11
fecha_creacion: 2026-07-27
fecha_actualizacion: 2026-10-18
estado: Aprobado
---

# Historia de Usuario — HU-[SIGLA]-[NNN]

Plantilla normativa de Historia de Usuario. Adapta íntegramente la estructura de [[Manual de Diligenciamiento Formato Historia de Usuario v.2]] (fuente de cliente, inmutable — P9) al modelo de entidades de esta wiki ([[ONTOLOGIA]]).

**No repite campos que ya viven en la Tarea del documento de Seguimiento** (DEC-25): se omiten del manual original "Id. Herramienta de Proyecto" (Jira/Azure — P2, sin herramientas externas), "Puntos de historia", "Estado" y "Sprint/Fecha inicio Sprint". Esos tres últimos ya son campos de la Tarea (`MODELO-REQUERIMIENTO.md` §2.1 y §2.2); duplicarlos aquí rompería la propagación de un solo dato dueño.

---

## 1. Identificación de la Historia de Usuario

| Campo | Valor |
| :--- | :--- |
| **Id. Historia de Usuario** | `HU-[SIGLA]-[NNN]` (ej. `HU-DEMO-001`) |
| **Nombre** | `[Título breve y descriptivo de la acción principal]` |
| **Requerimiento padre** | `[[SIGLA]-REQ-[NNN]]` |
| **Paso de Flujo** | `P-[NN]` — ver `plantilla-flujo-funcional.md` |
| **Épica / Feature** | `Épica: [nombre] / Feature: [nombre]` — contexto descriptivo. No genera documento propio (P11). |
| **Actor** | `[Rol reconocido del negocio — nunca genérico "usuario"]` |
| **Prioridad** | `Alta / Media / Baja` |
| **Dependencias HU** | `[Listar HU de las que depende, o "Ninguna"]` |
| **Pre-condiciones** | `[Servicios o estados previos requeridos, o "Ninguna". Muchas dependencias es señal de alerta.]` |

---

## 2. Escenario de la HU

| Pregunta clave | Contenido |
| :--- | :--- |
| **Como** (rol) | `[Actor específico, reconocido en el negocio]` |
| **Quiero** (objetivo) | `[Acción concreta en verbo infinitivo — el QUÉ, no el CÓMO técnico. Una sola funcionalidad.]` |
| **Para** (beneficio) | `[Valor tangible desde la perspectiva del usuario o del negocio]` |

---

## 3. Reglas de negocio

Restricciones o políticas obligatorias del dominio. Sin detalle técnico de implementación. **Máximo 15.**

| ID | Descripción |
| :---: | :--- |
| `RN-01` | `[Restricción o política de negocio, enunciado verificable]` |

---

## 4. Criterios de aceptación

Formato Gherkin. **Máximo 15.** Deben incluir obligatoriamente **happy path**, **unhappy path** (errores/validaciones) y **escenarios alternativos**. Cada criterio es independiente de los demás.

| No. | Dado que | Cuando | Entonces |
| :---: | :--- | :--- | :--- |
| `01` | `[Contexto o estado previo]` | `[Acción que dispara el comportamiento]` | `[Resultado observable y verificable]` |

---

## 5. Prototipos / Mockup

`[Enlace a herramienta de prototipado, imagen insertada, o "No aplica" / "Pendiente de diseño UX"]`. Los prototipos son orientativos, no contractuales.

---

## 6. Flujo

Enlace al documento de Flujo que contiene el diagrama Mermaid y la secuencia de pasos (`plantilla-flujo-funcional.md`). Esta sección **no transcribe** el diagrama, solo referencia:

- **Flujo:** `[[nombre-del-documento-de-flujo]]`
- **Paso de esta HU dentro del flujo:** `P-[NN]`

---

## 7. Web Service asociado

Solo referencia el **ID canónico** del Web Service (DEC-32, B2-T09). Prohibido escribir URLs, métodos HTTP o detalle técnico en esta sección: ese detalle vive únicamente en la ficha del WS (`plantilla-contrato-ws.md`).

| Web Service | Rol en este paso |
| :--- | :--- |
| `[[ws-sigla-nnn-nombre]]` | `[Para qué lo invoca esta HU, en una línea]` |

Si esta HU no invoca ningún Web Service, esta sección se omite (P11).

---

## 8. Datos de entrada (input) y datos de salida (output)

| Campo | Tipo (genérico) | Obligatoriedad | Longitud | Detalle |
| :--- | :---: | :---: | :--- | :--- |
| `[nombre_campo]` | `Texto / Numérico / Fecha / Booleano / Lista / Archivo` | `Obligatorio / Opcional` | `[Máx. N caracteres, N dígitos, etc.]` | `[Máscara, valores permitidos, valor por defecto]` |

Si el requerimiento es de integración técnica, detallar estos campos como los de una API. Si es funcional, priorizar interacción y validaciones de interfaz.

---

## 9. Notas

`[Observaciones adicionales no contempladas arriba — en particular, requerimientos no funcionales.]`

---

## 10. Anexos

Solo si aplica.

| Tipo de documento | Nombre del documento | Página / Numeral | Ubicación | Autor | Fecha de envío | Observación |
| :--- | :--- | :---: | :--- | :--- | :---: | :--- |
| `[Técnico / Manual / Normativa]` | `[Título exacto]` | `[Sección]` | `[[wikilink — nunca ruta absoluta]]` | `[Autor]` | `[AAAA-MM-DD]` | `[Nota]` |

---

## 11. Aprobadores

Control de versiones y trazabilidad. Los campos de control quedan **vacíos para llenado manual**; el agente no los completa por su cuenta.

| Versión | Fecha | Autor | Revisado por | Aprobado por | Rol del aprobador | Descripción de cambio | Estado |
| :---: | :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| `V1` | `[AAAA-MM-DD]` | `[Vacío]` | `[Vacío]` | `[Vacío]` | `[Vacío]` | `[Vacío]` | `Pendiente` |

El agente solo asume el rol de aprobador cuando el PO se lo indique explícitamente para esa HU puntual.

---

## Ejemplo de referencia

Instancia ficticia y genérica, conforme a DEC-16. No corresponde a ningún cliente real.

**HU-DEMO-001 — Reservar sala de reuniones**
Requerimiento padre: `DEMO-REQ-001` · Paso: `P-02` · Actor: Empleado registrado · Prioridad: Alta

- **Como** empleado registrado, **quiero** reservar una sala de reuniones disponible, **para** coordinar reuniones sin cruzar horarios con otro equipo.
- **RN-01:** No se admite una reserva con menos de dos horas de anticipación.
- **CA-01 (happy path):** Dado que la sala está libre en el horario elegido, cuando confirmo la reserva, entonces el sistema la registra y notifica al solicitante.
- **CA-02 (unhappy path):** Dado que la sala ya está reservada en ese horario, cuando intento confirmar, entonces el sistema rechaza la reserva y muestra el conflicto.
- **WS asociado:** `[[ws-demo-001-consulta-disponibilidad-salas]]` — consulta de franjas libres por sala.

---

## Reglas de uso

1. **Evaluación previa obligatoria.** Antes de redactar, el agente confirma si actor, lógica de negocio y casos de falla están claros. Si hay vacíos, se detiene y pregunta (P5) — no completa por suposición.
2. **Tipos de dato genéricos.** Las tablas técnicas usan siempre `Texto`, `Numérico`, `Booleano`, `Fecha`, nunca tipos de un lenguaje de programación específico.
3. **Sigla mínima de 4 letras.** Gana la regla de `ONTOLOGIA.md` §4.1; se descarta explícitamente cualquier criterio de sigla de 3 letras.
4. **Máximo 15 reglas de negocio y máximo 15 criterios de aceptación** (DEC-10, regla 28 de `CLAUDE.md`). Si se supera, el agente se detiene y pregunta al PO cómo dividirla.
5. **Nunca URLs ni detalle técnico de integración en el cuerpo de la HU** (DEC-32). Solo el ID canónico del WS.
6. **Las secciones vacías se omiten**, no se dejan con marcadores sin llenar (P11).
7. **Los campos de control de la sección 11 quedan vacíos** hasta que un humano los diligencie.
