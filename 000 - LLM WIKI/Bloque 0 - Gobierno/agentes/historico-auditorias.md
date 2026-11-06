---
id_documento: HISTORICO-AUDITORIAS-AGENTES
tipo_documento: log-agentes
bloque: Bloque 0 - Gobierno
fecha_creacion: 2026-07-28
fecha_actualizacion: 2026-11-05
estado: Aprobado
---

# Histórico de auditorías de los subagentes

Log append-only de cada corrida de los 5 agentes de auditoría (`conexiones-vault`, `organizador-carpetas`, `vista-grafica`, `logica-requerimientos`, `auditoria-de-rol`). Cada corrida agrega una fila nueva al final — nunca se borra ni se reescribe una fila existente. El detalle completo de la corrida más reciente de cada agente vive en [[reporte-actual]]; este log es solo el rastro histórico de cuándo corrió cada uno y con qué resultado.

**Regla de mantenimiento:** cada agente, al terminar su corrida, agrega su propia fila aquí. Nunca modifica una fila ajena. Si el mismo agente corre dos veces el mismo día, la segunda corrida complementa la fila de esa fecha (se edita esa misma fila para sumar los hallazgos nuevos) en vez de crear una fila duplicada.

## Log

| Fecha | Agente | Alcance | Críticos | Menores | Resumen de la corrida |
| :---: | :--- | :--- | :---: | :---: | :--- |
| `2026-10-18` | `conexiones-vault` | Bóveda completa (`000` + `100`) | `0` | `0` | Corrida inicial detectó duplicado `Bloque 0/llm-wiki.md`, wikilink hacia `referencias-externas/` y referencias sin wikilink en bitácora de `DEMO-REQ-001`; remediados y verificados en segunda corrida del día (`0 Críticos, 0 Menores`). |
| `2026-10-18` | `organizador-carpetas` | Bóveda completa (`000` + `100`) | `0` | `0` | Verificada estructura de raíz, eliminación de duplicados, incorporación de `GEMINI.md` puente (DEC-10) y alineación de `ONTOLOGIA.md` §4.3 con `hoja-principal-demo-req-001.md` (`0 Críticos, 0 Menores`). |
| `2026-10-18` | `vista-grafica` | Bóveda completa (`000` + `100`) | `0` | `0` | Verificados dos componentes conexos sin cruces entre guía y proyecto activo, cero páginas huérfanas, cumplimiento de DEC-09 y configuración de `colorGroups` en `.obsidian/graph.json` (`0 Críticos, 0 Menores`). |
| `2026-10-18` | `logica-requerimientos` | `DEMO-REQ-001` + Plantillas B1/B2 | `0` | `0` | Unificado tope de 15 RN y 15 CA en `plantilla-historia-de-usuario.md` (DEC-10), incluido `Sin iniciar` en `GLOSARIO.md`, corregidos prefijos `DEMO-REQ-001` en plantillas y sincronizadas fechas y trazabilidad de `DEMO-REQ-001` (`0 Críticos, 0 Menores`). |
| `2026-10-18` | `auditoria-de-rol` | `DEMO-REQ-001` | `0` | `0` | Simulación completa del actor `Empleado registrado` (`P-01` a `P-05`); homologado campo `fecha` entre HU y WS, documentados campos de salida en sección 8 de `HU-DEMO-001` y asignada tarea EDT `3.2` a `P-04` y `P-05` (`0 Críticos, 0 Menores`). |
| `2026-11-05` | `conexiones-vault` | Bóveda completa (`000` + `100`) | `1` | `0` | Detectados 5 wikilinks ilustrativos en `Bloque 2` (`plantilla-flujo-funcional`, `plantilla-historia-de-usuario`, `REGLA-IDENTIFICADOR-WS`) que cruzan indebidamente hacia `DEMO-REQ-001`; 0 enlaces rotos (`1 Crítico, 0 Menores`). |
| `2026-11-05` | `organizador-carpetas` | Bóveda completa (`000` + `100`) | `0` | `0` | Estructura de raíz, normas MAYÚSCULAS-CON-GUIONES, plantillas e instancias de DEMO-REQ-001 cumplen 100% las convenciones vigentes (`0 Críticos, 0 Menores`). |
| `2026-11-05` | `vista-grafica` | Bóveda completa (`000` + `100`) | `1` | `1` | Detectado cruce Guía ↔ Proyecto Activo por wikilinks de Bloque 2 a DEMO-REQ-001; detectada página huérfana en raíz `GEMINI.md` desconectada del grafo (`1 Crítico, 1 Menor`). |
