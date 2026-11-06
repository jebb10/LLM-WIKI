# LLM Wiki — Base de conocimiento agnóstica para agentes de código

Una base de conocimiento en Markdown puro que le enseña a un agente de código LLM (Claude Code, Codex, o similar) cómo llevar un proyecto de software con **trazabilidad total**: requerimientos, flujos, historias de usuario, reglas de negocio, contratos de servicios, tareas y bloqueos — todo interconectado, todo consultable en lenguaje natural.

Se clona, se abre el agente, y el agente entiende el objetivo. No hay instalación, ni dependencias, ni scripts.

---

## El problema que resuelve

En un proyecto de software real, la información de requerimientos se dispersa: una regla de negocio se define en una reunión, se escribe en un documento de Word, se contradice tres semanas después en un chat, y nadie sabe cuál de las dos versiones llegó al desarrollo. Cuando alguien pregunta *"¿qué tenemos pendiente hoy?"*, la respuesta se reconstruye a mano.

Este sistema convierte esa dispersión en un artefacto que **se compila y se mantiene vigente**. La señal única de éxito: preguntarle al agente y recibir todas las tareas pendientes del día, al día, sin reconstruir nada.

---

## Las 5 preguntas que responde

| # | Funcionalidad | Responde a |
|:-:|:---|:---|
| 1 | Reporte de pendientes del día | ¿Qué tenemos pendiente hoy? ¿Qué nos hace falta? |
| 2 | Cálculo de avance | ¿Qué porcentaje tiene el requerimiento X? (con fecha de corte declarada) |
| 3 | Resumen semanal | ¿Cuáles fueron los avances de la última semana? |
| 4 | Detección de contradicciones | ¿Qué se contradice dentro de un requerimiento o entre requerimientos? |
| 5 | Auditoría de rol | Recorrer el flujo como un usuario y decir qué paso no está bien documentado |

---

## Cómo funciona

El modelo es una jerarquía funcional estricta de 5 niveles:

```
Requerimiento (1:N) → Flujo (1:N) → Paso de Flujo (1:N) → Historia de Usuario (1:N) → Regla de Negocio
                                          └─ (0:N) Web Service
```

Cada entidad tiene un prefijo canónico, un lugar único donde vive, y una plantilla normativa que la define. Una tarea nunca es un archivo: es una fila. Un stopper nunca es un archivo: es una fila. El sistema prefiere un campo antes que un documento nuevo.

Sobre eso operan **11 principios no negociables**. Los dos más importantes para entender el diseño:

- **Ante conflicto, el agente se detiene y pregunta.** Nunca elige entre dos versiones de un dato ni corrige un hallazgo sin aprobación. Detecta y describe; la decisión es humana.
- **Cero dependencias externas.** Solo Markdown nativo y el agente. Sin plugins, sin scripts, sin servicios.

---

## Quickstart

1. **Clona el repositorio** y abre la carpeta con tu agente de código (Claude Code, Google Antigravity, Gemini CLI, Cursor o Codex).
2. **Abre `CLAUDE.md`.** Es la fuente de verdad operativa: el agente no necesita ningún otro documento para operar. Si usas Claude Code se carga automáticamente; si usas Antigravity / Gemini CLI, `GEMINI.md` actúa como puente automático hacia `CLAUDE.md`.
3. **Sigue el checklist de arranque** en `000 - LLM WIKI/Bloque 0 - Gobierno/CHECKLIST-ARRANQUE-PROYECTO-NUEVO.md` para instanciar la wiki sobre tu propio proyecto.

Para ver el sistema funcionando antes de tocar nada, revisa `100 - PROYECTO ACTIVO/002 - Requerimientos/DEMO-REQ-001/`: un requerimiento ficticio instanciado de punta a punta (hoja principal, seguimiento con stopper activo, flujo con diagrama Mermaid, historia de usuario y dos contratos de servicio).

**Opcional:** abre la carpeta como bóveda en [Obsidian](https://obsidian.md) para navegar los wikilinks y ver la vista de grafo. No es obligatorio — todo es Markdown legible en cualquier editor.

---

## Los 6 subagentes de auditoría

En `.claude/agents/` vienen 6 subagentes de solo lectura que vigilan la integridad de la bóveda. Se invocan **manualmente por nombre**; ninguno se dispara solo, y ninguno corrige nada.

| Agente | Qué audita |
|:---|:---|
| `conexiones-vault` | Wikilinks rotos, rutas absolutas prohibidas, referencias a páginas inexistentes |
| `organizador-carpetas` | Estructura de carpetas y convención de nombres de archivo |
| `vista-grafica` | Forma del grafo: páginas huérfanas y enlaces que rompen la topología esperada |
| `logica-requerimientos` | Consistencia interna de un requerimiento y uso correcto de vocabularios cerrados |
| `auditoria-de-rol` | Simula un usuario recorriendo el flujo y señala los vacíos de documentación |
| `auditoria-completa` | Orquesta los 3 primeros y consolida el resultado |

Su salida siempre va a los mismos dos archivos (`agentes/reporte-actual.md` y `agentes/historico-auditorias.md`) — nunca crean un reporte nuevo por corrida.

---

## Topología del grafo

El grafo está diseñado para verse limpio, en **dos grupos separados sin cruces**:

1. **Guía del agente** (`000 - LLM WIKI/`) — documentos normativos y plantillas, enlazados entre sí vía sus índices.
2. **Proyecto activo** (`100 - PROYECTO ACTIVO/`) — por cada requerimiento, sus documentos enlazan hacia la hoja principal de ese requerimiento (con texto plano entre ellos, nunca wikilink); solo la hoja principal enlaza al cronograma consolidado. Única excepción: el documento de Seguimiento sí enlaza con wikilinks reales a HU/WS/Flujo en su tabla de trazabilidad y su bitácora, porque de eso depende la propagación de cambios y la auditoría de rol.

Ninguna página queda huérfana: si un documento no tiene ninguna relación real, o se conecta o no debería existir.

---

## Estructura del repositorio

```
├── CLAUDE.md                      # Fuente de verdad operativa del agente
├── GEMINI.md                      # Puente ligero de compatibilidad (Antigravity / Gemini CLI → CLAUDE.md)
├── SPEC.md                        # Material fundacional: alcance y 20 casos de aceptación
├── .claude/agents/                # Los 6 subagentes de auditoría
├── 000 - LLM WIKI/                # La guía normativa
│   ├── Bloque 0 - Gobierno/       # Visión, principios, bitácora, checklist de arranque
│   ├── Bloque 1 - Modelo de requerimiento/   # Modelo + 5 plantillas
│   └── Bloque 2 - Ontología y relaciones/    # Ontología, estándares + 3 plantillas
├── 100 - PROYECTO ACTIVO/         # El proyecto en curso (trae DEMO-REQ-001 de ejemplo)
└── referencias-externas/          # Material de inspiración de terceros
```

---

## Estado del proyecto

El modelo está **cerrado**: principios, ontología, jerarquía de entidades y plantillas normativas ya no se rediseñan. El sistema se usó en producción llevando cerca de 26 requerimientos de un proyecto web de una compañía de seguros, con seguimiento de tareas, stoppers y proyección de entregas. Este repositorio es la versión agnóstica de ese sistema, sin ningún dato del cliente.

---

## Licencia y autoría

Diseñado y construido por **Johan Esteban Benítez Bermúdez**.

- GitHub: [@jebb10](https://github.com/jebb10)
- LinkedIn: [Johan Esteban Benítez Bermúdez](https://www.linkedin.com/in/johan-esteban-benitez-bermudez/)

El patrón conceptual en el que se inspira está acreditado en `referencias-externas/llm-wiki.md`.
