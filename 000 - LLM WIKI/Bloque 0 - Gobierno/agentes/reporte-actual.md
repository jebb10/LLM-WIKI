---
id_documento: REPORTE-ACTUAL-AGENTES
tipo_documento: reporte-agentes
bloque: Bloque 0 - Gobierno
fecha_creacion: 2026-07-28
fecha_actualizacion: 2026-10-18
estado: Aprobado
---

# Reporte actual de los subagentes de auditoría

Estado de la corrida más reciente de cada uno de los 5 agentes de auditoría (`conexiones-vault`, `organizador-carpetas`, `vista-grafica`, `logica-requerimientos`, `auditoria-de-rol`). Cada agente, al terminar, reemplaza por completo su propia sección — nunca toca la sección de otro agente. El rastro histórico de todas las corridas anteriores vive en [[historico-auditorias]].

**Resultado de estructura ideal verificada:**

```
LLM WIKI JB (raíz)
├── CLAUDE.md
├── GEMINI.md
├── SPEC.md
├── README.md
├── LICENSE
├── .obsidian/
├── .claude/
├── 000 - LLM WIKI/
│   ├── Bloque 0 - Gobierno/
│   │   ├── 00-VISION.md
│   │   ├── CONVENCIONES-ESCRITURA.md
│   │   ├── INDICE-DOCUMENTOS-GUIA.md
│   │   ├── LEEME-GOBIERNO.md
│   │   ├── CHECKLIST-ARRANQUE-PROYECTO-NUEVO.md
│   │   ├── BITACORA-DECISIONES.md
│   │   └── agentes/
│   │       ├── reporte-actual.md
│   │       └── historico-auditorias.md
│   ├── Bloque 1 - Modelo de requerimiento/
│   │   ├── LEEME-MODELO-DE-REQUERIMIENTO.md
│   │   ├── MODELO-REQUERIMIENTO.md
│   │   ├── plantilla-hoja-principal-requerimiento.md
│   │   ├── plantilla-seguimiento-requerimiento.md
│   │   ├── plantilla-conclusion-requerimiento.md
│   │   ├── plantilla-requerimiento-cliente.md
│   │   └── plantilla-mapeo-excepcion-jerarquia.md
│   └── Bloque 2 - Ontología y relaciones/
│       ├── LEEME-ONTOLOGIA-Y-RELACIONES.md
│       ├── ONTOLOGIA.md
│       ├── GLOSARIO.md
│       ├── ESTANDAR-FRONTMATTER-Y-FECHAS.md
│       ├── REGLA-IDENTIFICADOR-WS.md
│       ├── plantilla-historia-de-usuario.md
│       ├── plantilla-flujo-funcional.md
│       ├── plantilla-contrato-ws.md
│       └── Manual de Diligenciamiento Formato Historia de Usuario v.2.md
├── 100 - PROYECTO ACTIVO/
│   ├── 001 - Cronograma de Requerimientos/
│   │   ├── 000 - Plan de Trabajo - Cronograma de Requerimientos.md
│   │   └── 001 - Requerimientos Cerrados y Pausados.md
│   ├── 002 - Requerimientos/
│   │   ├── INDICE-DOCUMENTOS-REQUERIMIENTOS.md
│   │   └── DEMO-REQ-001/
│   │       ├── hoja-principal-demo-req-001.md
│   │       ├── seguimiento-demo-req-001.md
│   │       ├── flujo-demo-001-reserva-de-sala.md
│   │       ├── hu-demo-001-reservar-sala.md
│   │       ├── ws-demo-001-consulta-disponibilidad-salas.md
│   │       └── ws-demo-002-crear-reserva.md
│   ├── _entrada-actualizaciones/
│   │   └── LEEME-ENTRADA-ACTUALIZACIONES.md
│   ├── 004 - Canvas/
│   └── 005 - Files/
└── referencias-externas/
    └── llm-wiki.md
```

---

## 1. `conexiones-vault`

- **Fecha de corrida:** `2026-10-18`
- **Alcance:** Guía del agente (`000 - LLM WIKI/`, `CLAUDE.md`, `SPEC.md`) y Proyecto activo (`100 - PROYECTO ACTIVO/`).
- **Resultado:** `0 Críticos · 0 Menores`

| Espacio | Wikilinks verificados | Enlaces rotos | Rutas absolutas (`file:///`) | Cruces prohibidos de frontera |
| :--- | :---: | :---: | :---: | :---: |
| `000 - LLM WIKI/` + Raíz | 48 | 0 | 0 | 0 |
| `100 - PROYECTO ACTIVO/` | 24 | 0 | 0 | 0 |

**Observación de cierre:** Se eliminó el archivo duplicado `Bloque 0 - Gobierno/llm-wiki.md`, se reemplazó el wikilink hacia `referencias-externas/llm-wiki` en [[INDICE-DOCUMENTOS-GUIA]] por referencia en código plano (`referencias-externas/llm-wiki.md`), y se normalizaron todos los enlaces de la bitácora de `seguimiento-demo-req-001.md` con wikilinks internos del propio requerimiento.

---

## 2. `organizador-carpetas`

- **Fecha de corrida:** `2026-10-18`
- **Alcance:** Raíz del repositorio, `000 - LLM WIKI/` y `100 - PROYECTO ACTIVO/`.
- **Resultado:** `0 Críticos · 0 Menores`

| Verificación | Estado | Detalle |
| :--- | :---: | :--- |
| Estructura de carpetas de raíz | Cumple | `000 - LLM WIKI/`, `100 - PROYECTO ACTIVO/`, `referencias-externas/`, `.obsidian/`, `.claude/` y artefactos de raíz (`CLAUDE.md`, `GEMINI.md`, `SPEC.md`, `README.md`, `LICENSE`). |
| Nomenclatura de normas (`MAYUSCULAS-CON-GUIONES.md`) | Cumple | 100 % de normas en Bloques 0, 1 y 2 cumplen (con las excepciones declaradas `00-VISION.md` y `LEEME-*.md`). |
| Nomenclatura de plantillas (`plantilla-*.md`) | Cumple | 8 plantillas normativas en minúsculas con guiones. |
| Nomenclatura de instancias (`tipo-sigla-nnn-nombre.md`) | Cumple | `ONTOLOGIA.md` §4.3 alineado con `hoja-principal-demo-req-001.md`; las 6 fichas de `DEMO-REQ-001` cumplen. |

---

## 3. `vista-grafica`

- **Fecha de corrida:** `2026-10-18`
- **Alcance:** Topología de dos componentes conexos separados (`000 - LLM WIKI/` vs `100 - PROYECTO ACTIVO/`) y configuración visual `.obsidian/graph.json`.
- **Resultado:** `0 Críticos · 0 Menores`

| Métrica de Grafo | Guía del Agente (`000 - LLM WIKI/`) | Proyecto Activo (`100 - PROYECTO ACTIVO/`) |
| :--- | :---: | :---: |
| Páginas huérfanas | 0 | 0 |
| Cruces entre guía y proyecto | 0 | 0 |
| Violaciones al patrón estrella (DEC-09) | No aplica | 0 (cruces HU↔Flujo↔WS en texto plano; excepción de `seguimiento-demo-req-001` aplicada) |
| Grupos de color (`.obsidian/graph.json`) | Configurados (3 grupos semánticos) | Configurados |

---

## 4. `logica-requerimientos`

- **Fecha de corrida:** `2026-10-18`
- **Requerimiento auditado:** `DEMO-REQ-001` (y consistencia normativa contra Bloques 1 y 2).
- **Resultado:** `0 Críticos · 0 Menores`

| Regla verificada | Estado | Evidencia |
| :--- | :---: | :--- |
| Vocabulario cerrado de `Estado Macro` | Cumple | `GLOSARIO.md`, `ONTOLOGIA.md` y `MODELO-REQUERIMIENTO.md` unificados (`Sin iniciar`, `En curso`, `Bloqueado`, `Cerrado en Producción (Dormido)`). |
| Límite máximo de RN y CA por HU | Cumple | Unificado en **máximo 15 RN y 15 CA** tanto en `CLAUDE.md` (regla 28) como en `plantilla-historia-de-usuario.md` (DEC-10). |
| Sincronía de fechas y antigüedad de stoppers | Cumple | `fecha_actualizacion: 2026-07-29` en frontmatter y cabecera de `seguimiento-demo-req-001.md`; `STP-01` con origen `2026-07-15` y antigüedad exacta de `14 días`. |
| Tabla de trazabilidad completa | Cumple | `P-01` a `P-05` mapeados a `RN-01..RN-04` y tareas EDT `3.1` y `3.2`. |
| Prefijos canónicos en ejemplos de plantillas | Cumple | Corregidos `REQ-DEMO-001` → `DEMO-REQ-001` y `MIGR-REQ-001` → `DEMO-REQ-001` en Bloques 1 y 2. |

---

## 5. `auditoria-de-rol`

- **Fecha de corrida:** `2026-10-18`
- **Requerimiento auditado:** `DEMO-REQ-001` (recorrido simulado del actor `Empleado registrado` desde `P-01` hasta `P-05`).
- **Resultado:** `0 Críticos · 0 Menores`

| Paso del flujo | Actor | HU / WS verificados | Resultado del recorrido |
| :---: | :--- | :--- | :--- |
| `P-01` | Empleado registrado | `HU-DEMO-001` · `WS-DEMO-001` | Entrada (`id_sala`, `fecha`) y salida (`capacidad`, `franjas_libres`) documentadas extremo a extremo, incluido manejo de timeout > `2.0s` (`CA-06`). |
| `P-02` | Sistema | Decisión técnica | Punto de evaluación de franja libre documentado en flujo y tabla de trazabilidad. |
| `P-03` | Empleado registrado | `HU-DEMO-001` · `WS-DEMO-002` | Entrada (`id_sala`, `fecha`, `hora_inicio`, `duracion_minutos`, `motivo`), reglas (`RN-01` a `RN-04`) y salida (`id_reserva`, `estado_reserva`) completas. |
| `P-04` | Sistema | `HU-DEMO-001` | Rechazo por conflicto (`HTTP 409`, `CA-02`) y por anticipación (`HTTP 422`, `CA-03`) documentado con retorno al paso de consulta. |
| `P-05` | Sistema | `HU-DEMO-001` | Notificación al solicitante (`notificacion_enviada`, `id_reserva`, `CA-01`) y tarea EDT `3.2` trazadas. |
