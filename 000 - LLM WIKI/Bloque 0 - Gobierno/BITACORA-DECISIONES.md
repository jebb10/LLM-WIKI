---
id_documento: BITACORA-DECISIONES-B0
tipo_documento: bitacora
bloque: Bloque 0 - Gobierno
principios_aplicados: [P1, P4, P5, P10, P11]
fecha_creacion: 2026-07-01
fecha_actualizacion: 2026-10-18
estado: Aprobado
---

# Bitácora de Decisiones de Diseño y Arquitectura

Registro histórico de decisiones de arquitectura, estructura y operación de la LLM Wiki. **No tiene precedencia sobre `CLAUDE.md`**: `CLAUDE.md` es la fuente de verdad vigente sobre cómo operar la bóveda (ver su sección "Regla de precedencia"); esta bitácora solo deja rastro de cuándo y por qué se tomó cada decisión ya reflejada en `CLAUDE.md` o en los documentos normativos.

**Formato:** índice de una línea por decisión vigente — `[DEC-NN] Enunciado — Ref: Principio/Tarea`. No se conserva el detalle de alternativas descartadas ni la justificación extensa de cada decisión histórica. Toda decisión sigue siendo citable por su ID desde cualquier otro documento.

**Regla de mantenimiento:** las decisiones nuevas se agregan como fila de índice al final, ordenadas por fecha. Es responsabilidad del agente agregar la fila correspondiente al cerrar cualquier sesión en la que se tome una decisión de gobierno nueva. Una decisión superada por otra se marca `(superada por DEC-NN)`, nunca se borra.

---

## Nota sobre los identificadores históricos

Varias plantillas y documentos normativos citan decisiones con IDs de la forma `DEC-NN` y definiciones `DP-NN` (ej. `DEC-16`, `DEC-25`, `DP-27`). Esos identificadores provienen del historial de diseño privado que precedió a la publicación de este repositorio y **su detalle no se reproduce aquí**. Cada cita conserva junto a ella el enunciado de la regla que aplica, así que la regla se entiende sin necesidad de resolver el ID. El índice de abajo arranca en `DEC-01` y registra únicamente las decisiones tomadas sobre la versión publicable.

---

## Índice de decisiones

| ID | Fecha | Decisión | Ref. |
| :---: | :---: | :--- | :--- |
| `DEC-01` | `2026-07-28` | Una sola bóveda de Obsidian con dos carpetas hermanas (`000 - LLM WIKI/` guía, `100 - PROYECTO ACTIVO/` proyecto), en vez de dos bóvedas anidadas con su propio `.obsidian`. Motivo: quien clone el repositorio ve el grafo completo de una sola vez y los subagentes auditan ambos espacios en una corrida. La frontera entre los dos espacios pasa a ser convención de grafo, no barrera técnica. | P1, P10 |
| `DEC-02` | `2026-07-28` | La carpeta del proyecto en curso se llama `100 - PROYECTO ACTIVO/`, nombre genérico, en vez del nombre del cliente. Motivo: agnosticidad — el repositorio debe servir a cualquier proyecto de software sin renombrar rutas en la documentación. | P1, CP-20 |
| `DEC-03` | `2026-07-28` | Los 6 subagentes de auditoría se empaquetan dentro del repositorio en `.claude/agents/`, no en la configuración global de la máquina. Motivo: sin esto, quien clone el repositorio no obtiene ningún agente y la funcionalidad descrita en `CLAUDE.md` no existe en la práctica. | P2 |
| `DEC-04` | `2026-07-28` | Se conserva un requerimiento ficticio completo (`DEMO-REQ-001`, reserva de salas) instanciado de punta a punta como ejemplo de referencia permanente del repositorio. Motivo: demuestra el modelo funcionando sin exponer datos reales; el checklist de arranque indica cómo eliminarlo al iniciar un proyecto propio. | P4, CP-19 |
| `DEC-05` | `2026-07-28` | Regla dura nueva: este repositorio es publicable y nunca lleva datos reales de cliente (ni nombres, ni personas, ni URLs de servicios reales, ni rutas absolutas de una máquina). El trabajo sobre proyectos reales vive en una copia privada. | P1, P9 |
| `DEC-06` | `2026-07-28` | Se crea `CHECKLIST-ARRANQUE-PROYECTO-NUEVO.md` como documento normativo de Bloque 0. Motivo: `SPEC.md` lo exigía en CP-19 pero no existía como archivo; es la pieza que habilita la replicabilidad del sistema sobre un proyecto nuevo. | P4, CP-19 |
| `DEC-07` | `2026-07-28` | `SPEC.md` pasa a referenciar los demás documentos con wikilinks `[[...]]` en vez de nombres en backticks. Motivo: cumplía a medias la propia regla dura de wikilinks y quedaba aislado del grafo pese a referenciar 25 documentos. | P2 |
| `DEC-08` | `2026-07-28` | Se agrega `README.md` en la raíz como portada para lectores humanos, separado de `CLAUDE.md`, que sigue siendo la única fuente de verdad operativa del agente. Motivo: un visitante del repositorio no debería leer reglas operativas del agente para entender qué es el proyecto. | P11 |
| `DEC-09` | `2026-07-29` | Regla dura aclarada: dentro de un requerimiento, los cruces HU↔Flujo↔WS se referencian en texto plano con el ID (nunca wikilink) — solo la hoja principal recibe wikilinks reales desde ellos. Única excepción: el documento de Seguimiento sí usa wikilinks reales hacia HU/WS/Flujo en su tabla de trazabilidad y en la columna "Documentos afectados" de su bitácora, por mandato de `plantilla-seguimiento-requerimiento.md` — sin esos enlaces no funcionan la propagación de cambios ni la auditoría de rol. Motivo: `vista-grafica` encontró la violación en `DEMO-REQ-001`, el ejemplo público del patrón. | P1, CP-16 |
| `DEC-10` | `2026-10-18` | Unificación del límite de Reglas de Negocio y Criterios de Aceptación en `plantilla-historia-de-usuario.md` a **máximo 15** (alineado con la regla 28 de `CLAUDE.md`), creación de `GEMINI.md` en la raíz como puente ligero de compatibilidad multi-agente (Claude Code + Antigravity/Gemini CLI) sin duplicar contenido normativo (P4, P11), y remediación integral de los hallazgos de los 5 subagentes de auditoría sobre `DEMO-REQ-001` y plantillas de Bloques 1 y 2. | P4, P5, P11 |

