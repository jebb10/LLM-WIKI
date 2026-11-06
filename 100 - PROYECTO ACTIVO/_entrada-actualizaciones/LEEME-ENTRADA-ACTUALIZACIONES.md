---
id_documento: LEEME-ENTRADA-ACTUALIZACIONES
tipo_documento: indice-carpeta
fecha_creacion: 2026-07-28
fecha_actualizacion: 2026-07-28
estado: Aprobado
---

# Buzón de intake

Aquí el PO deposita la información nueva **antes** de la sesión de trabajo: la Historia de Usuario redactada, la nota estructurada, o el documento original del cliente. El agente lo lee al iniciar la sesión del requerimiento correspondiente.

Los requerimientos destino se consultan en [[INDICE-DOCUMENTOS-REQUERIMIENTOS]] y su estado en [[000 - Plan de Trabajo - Cronograma de Requerimientos]].

---

## Cómo se usa

1. El PO deja el documento aquí, con el código del requerimiento destino en el nombre del archivo (ej. `DEMO-REQ-001 - nueva HU de cancelación.md`).
2. En la siguiente sesión de ese requerimiento, el agente lo lee como primer paso de la ingesta.
3. El agente pregunta explícitamente qué se debe actualizar o retirar antes de tocar nada — nunca asume el alcance del cambio.
4. Una vez ingerido, el documento sale de este buzón: o se archiva en `_fuente-cliente/` del requerimiento si es fuente inmutable del cliente (P9), o se elimina si su contenido ya quedó reflejado en las fichas.

---

## Reglas

- **Un documento, un requerimiento destino.** Si una nota podría pertenecer a dos requerimientos, el agente pregunta antes de escribir (CP-13).
- **Sin sustancia no hay página nueva.** Una nota sin objetivo, actor, regla ni decisión se devuelve para refinar o se descarta — no genera documento (P4, CP-12).
- **El buzón vacío es el estado normal.** Que quede vacío significa que todo lo entregado ya fue ingerido.

Actualmente el buzón está vacío.
