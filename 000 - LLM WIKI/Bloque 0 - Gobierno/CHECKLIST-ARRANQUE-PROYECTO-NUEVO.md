---
id_documento: CHECKLIST-ARRANQUE-B0
tipo_documento: norma
bloque: Bloque 0 - Gobierno
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P11
fecha_creacion: 2026-07-28
fecha_actualizacion: 2026-07-28
estado: Aprobado
---

# Checklist de Arranque — Proyecto Nuevo

Pasos exactos para instanciar esta wiki sobre un proyecto de software propio. Se sigue una sola vez por proyecto, en orden. Al terminar, el proyecto queda operativo sin improvisar y sin consultar conversaciones anteriores (CP-19).

**Regla de agnosticidad:** ninguna plantilla de esta wiki exige un campo que solo tenga sentido en el proyecto que inspiró el diseño (CP-20). Si al seguir este checklist encuentras un campo que no aplica a tu dominio, se omite — nunca se rellena con un valor inventado (P11, P5).

---

## 0. Antes de empezar — la salvaguarda

Si este repositorio es público o lo vas a publicar: **nunca lleva datos reales de cliente.** Ni nombres de empresa, ni personas, ni URLs de servicios reales, ni rutas absolutas de tu máquina. Si vas a llevar un proyecto real con información sensible, trabaja sobre una **copia privada** de esta bóveda y deja la versión publicable con el ejemplo `DEMO`.

---

## 1. Limpiar el ejemplo de referencia

1. Borra la carpeta `100 - PROYECTO ACTIVO/002 - Requerimientos/DEMO-REQ-001/` completa.
2. Vacía la tabla de requerimientos vigentes de `100 - PROYECTO ACTIVO/001 - Cronograma de Requerimientos/000 - Plan de Trabajo - Cronograma de Requerimientos.md`.
3. Vacía la sección de `DEMO-REQ-001` de `100 - PROYECTO ACTIVO/002 - Requerimientos/INDICE-DOCUMENTOS-REQUERIMIENTOS.md`.

No borres nada de `000 - LLM WIKI/`: esa es la guía normativa y se conserva intacta. Los ejemplos `DEMO` **dentro de las plantillas** también se conservan — son parte del molde.

---

## 2. Definir la sigla del primer requerimiento

- Mínimo **4 letras mayúsculas**, derivada del nombre funcional del requerimiento (no del cliente ni del proveedor).
- Si no hay una fuente clara para la sigla, el agente propone una y **espera aprobación explícita del PO** antes de crear la carpeta (regla 31 de [[CLAUDE]]).
- Una sigla por dominio funcional. Dos requerimientos independientes que compartan sigla se agrupan luego en `[SIGLA]-FAMILIA/`.

Ejemplos válidos: `RESE` (reservas), `FACT` (facturación), `DESP` (despachos).

---

## 3. Crear la carpeta del requerimiento

Crea `100 - PROYECTO ACTIVO/002 - Requerimientos/[SIGLA]-REQ-001/`.

Si el requerimiento nació de un documento del cliente, crea dentro `_fuente-cliente/` y deposita ahí el original **sin modificarlo nunca** (P9). Si no hay documento original, esa carpeta no se crea — es opcional.

---

## 4. Sesión de ingesta — qué pregunta el agente

La primera sesión sobre cualquier requerimiento es una **ingesta desde cero**, sin asumir que el contenido existente esté completo o vigente. El agente pregunta y espera respuesta antes de escribir:

1. ¿Cuál es el objetivo del requerimiento en dos líneas?
2. ¿Quiénes son los actores y qué decide cada uno?
3. ¿Qué reglas de negocio macro lo restringen?
4. ¿Qué integraciones o servicios externos necesita?
5. ¿Hay algo bloqueado hoy, y quién responde por ese bloqueo?
6. ¿Hay estimación de horas y fecha de corte?

Todo dato que el PO no tenga aún queda como `[PENDIENTE]` — a secas, sin variantes. La sesión sigue sobre el resto de la ficha; no se detiene por un campo faltante (regla 24 de [[CLAUDE]]).

---

## 5. Orden de diligenciamiento de las plantillas

Se instancia en este orden. Cada archivo se nombra `tipo-sigla-nnn-nombre.md`, todo en minúsculas.

| # | Documento | Plantilla | Cuándo |
| :-: | :--- | :--- | :--- |
| 1 | Hoja principal | [[plantilla-hoja-principal-requerimiento]] | Primero — es el hub del requerimiento. Se llena en paralelo, no de una sola vez (regla 29 de [[CLAUDE]]). |
| 2 | Seguimiento | [[plantilla-seguimiento-requerimiento]] | Inmediatamente después — aquí viven **todas** las tareas y stoppers. |
| 3 | Flujo funcional | [[plantilla-flujo-funcional]] | Cuando el recorrido esté claro. Siempre con diagrama Mermaid embebido. |
| 4 | Historia de Usuario | [[plantilla-historia-de-usuario]] | Una por funcionalidad. Cada HU exige su fila en la tabla de trazabilidad. |
| 5 | Ficha de Web Service | [[plantilla-contrato-ws]] | Una por endpoint. Nunca URLs ni detalle técnico fuera de esta ficha. |
| 6 | Conclusión | [[plantilla-conclusion-requerimiento]] | Solo al cerrar, cuando el Estado Macro pasa a `Cerrado en Producción`. |

Al instanciar una plantilla se **elimina su sección "Ejemplo de referencia"**. Si se deja, el documento queda con dos tablas del mismo dato.

---

## 6. Conectar el grafo

La topología esperada es de **dos grupos separados, sin cruces**:

- Los documentos de la guía (`000 - LLM WIKI/`) se enlazan entre sí vía sus hubs (`LEEME-*`, [[INDICE-DOCUMENTOS-GUIA]], [[CLAUDE]]).
- Los documentos de cada requerimiento enlazan hacia la **hoja principal de su propio requerimiento**. Solo la hoja principal enlaza además hacia el cronograma consolidado.
- Ningún wikilink cruza de la guía al proyecto activo ni entre dos requerimientos distintos.
- **Ninguna página queda huérfana.** Si un documento no tiene ninguna relación real, o se conecta o no debería existir.

Enlaza siempre con wikilinks `[[NombreDocumento]]`. Nunca rutas absolutas `file:///...` (P2).

---

## 7. Verificar con los subagentes

Con el primer requerimiento ya instanciado, invoca por nombre:

1. `auditoria-completa` — corre los 3 estructurales (`conexiones-vault` → `organizador-carpetas` → `vista-grafica`) y reporta enlaces rotos, desviaciones de nombre y huérfanas.
2. `logica-requerimientos` sobre tu requerimiento — verifica consistencia interna y vocabularios cerrados.
3. `auditoria-de-rol` sobre tu requerimiento — recorre el flujo como un usuario y señala qué falta para poder ejecutarlo.

Los 6 subagentes son de **invocación manual únicamente**: ninguno se dispara solo. Ninguno corrige nada — describen y esperan tu decisión (P5). Su salida vive en [[reporte-actual]] e [[historico-auditorias]].

---

## 8. Cierre del arranque

El proyecto está operativo cuando:

- [ ] El ejemplo `DEMO` está eliminado (o conservado a propósito como referencia).
- [ ] Existe `[SIGLA]-REQ-001/` con hoja principal y Seguimiento.
- [ ] El requerimiento tiene fila en el cronograma consolidado y en el índice de documentos.
- [ ] La tabla de trazabilidad tiene una fila por HU.
- [ ] `auditoria-completa` corre sin hallazgos Críticos.
- [ ] No hay ninguna página huérfana en el grafo.

A partir de aquí el trabajo es sesión por sesión: **un requerimiento por sesión**, el PO decide cuál, y toda actualización cierra con resumen visible y fila nueva en la bitácora del requerimiento.
