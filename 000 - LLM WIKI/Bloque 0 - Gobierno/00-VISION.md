---
id_documento: VISION-B0
tipo_documento: vision-producto
bloque: Bloque 0 - Gobierno
tarea_origen: B0-T01
principios_aplicados: [P1, P2, P3, P4, P5, P6, P7, P8, P9, P10, P11]
fecha_creacion: 2026-07-25
fecha_actualizacion: 2026-07-26
estado: Aprobado
---

# Visión del Producto — LLM Wiki

## 1. El producto en una frase
Un LLM Wiki con agente y skill que permite llevar un proyecto de software con claridad total de tareas y sin nunca perder la actualización de una definición en todos los documentos relacionados.

---

## 2. La señal única de éxito
Poder escribirle al agente: **"¿cuáles son las tareas pendientes de hoy?"** y recibir todo lo entregado previamente más el estado actualizado de tareas.

---

## 3. Criterio de rechazo (Definición de fracaso)
> **REGLA DE ORO / ANTI-OBJETIVO:** Cualquier entregable o propuesta que aumente el número de documentos, filas o estructuras **sin aumentar la trazabilidad navegable**, se descarta inmediatamente. Un sistema bonito sin relaciones claras es el fracaso declarado del proyecto.

---

## 4. Los 5 criterios de éxito
El producto está terminado cuando responde estas 5 preguntas de forma confiable:

1. **¿Qué tenemos pendiente hoy? ¿Qué nos hace falta?** (Tareas, pendientes y stoppers al día).
2. **¿Qué porcentaje de avance tiene el requerimiento X?** (Horas ejecutadas vs. estimadas con fecha del dato/corte).
3. **¿Cuáles fueron los principales avances de la última semana?** (Reporte automático desde el log).
4. **¿Qué contradicciones existen dentro de un requerimiento o entre requerimientos?** (Detección previa al desarrollo).
5. **"Actúa como un usuario, recorre el flujo documentado y dime qué paso o servicio no está bien documentado"** (Auditoría de completitud).

---

## 5. Los 11 principios del producto (Restricciones duras)

* **P1 - Un proyecto, una wiki:** Sin contaminación de contexto entre clientes ni entre proyectos.
* **P2 - Cero dependencias externas:** Todo vive en Markdown nativo/Git y el agente. Sin plugins o scripts externos.
* **P3 - Un solo escritor:** El PO y el agente escriben; el equipo lee.
* **P4 - La wiki compila, no acumula:** Si una fuente no aporta sustancia, no genera página nueva.
* **P5 - Ante conflicto, el agente se detiene y pregunta:** Nunca elige arbitrariamente entre dos versiones de un dato.
* **P6 - Todo en español:** Contenido, plantillas, Gherkin y reglas escritas en español.
* **P7 - El Excel conserva el detalle de horas y estado por área:** La wiki lleva un campo comparable y actualizado, no el detalle contable.
* **P8 - Alcance por requerimiento:** Historias de Usuario (HU), Flujo y Web Services (WS) pertenecen a un solo requerimiento.
* **P9 - La fuente original del cliente es inmutable:** Nunca se modifica la solicitud tal como llegó.
* **P10 - Economía de contexto:** Lectura en cascada (índice → log → resumen → detalle), nunca escaneo completo innecesario.
* **P11 - Mínimo número de documentos:** No se crea un documento nuevo si un campo o fila resuelve la necesidad. Cada carpeta tiene README actualizado.

---

## 6. Lo que NO es este producto
* **NO** es un reemplazo del Excel de bolsa de horas ni del cobro al cliente.
* **NO** es un dashboard visual.
* **NO** es un gestor de proyectos multiusuario.
* **NO** es un sistema de investigación abierta (sin scraping, sin agentes paralelos).
* **NO** es un analista de negocio (ejecuta, mantiene y señala hechos estructurales; no opina sobre calidad de negocio ni alcance).
* **NO** es un producto que aprenda solo (cada regla debe estar escrita en `CLAUDE.md` y en la bitácora).

---

## 7. Riesgos y Mitigaciones
> Cada riesgo está respaldado por una tarea concreta de mitigación. Ningún riesgo queda sin dueño asignado.

| ID Riesgo | Tipo | Impacto si ocurre | Mitigación (Tarea) |
| :---: | :---: | :--- | :--- |
| **R-01** | Crítico | Elimina el valor central del producto. | **B4-T03** crea verificación propia de la tabla; no se confía en que el agente la mantuvo. |
| **R-02** | Crítico | Es la definición de fracaso declarada por el PO. | **P11** como criterio de validación en toda tarea que genere plantillas; campo 'qué NO hacer' en cada tarea. |
| **R-03** | Alto | Pérdida de trabajo sin recuperación. | **B8-T05** habilita respaldo con Git, con confirmación antes de propagaciones masivas. |
| **R-04** | Alto | El proyecto se estanca en diseño permanente. | **v1 utilizable** declarada al cerrar B4-T04; los bloques 5 a 8 son mejora, no requisito para usarlo. |
| **R-05** | Alto | Exposición de información confidencial al publicar. | **B8-T02** nace ficticia desde el primer archivo; **B8-T07** verifica archivo por archivo antes de publicar. |
| **R-06** | Medio | El criterio de éxito 2 deja de ser confiable. | **B5-T02** obliga al agente a declarar siempre la fecha del corte y advertir si está viejo. |
| **R-07** | Medio | Se pierde el criterio de éxito 4. | **B6-T01** separa contradicción de desactualización y exige descartar diferencias de redacción. |
| **R-08** | Medio | Duplicidad silenciosa que rompe P7. | **B6-T05** incluye la verificación de P7 en el chequeo de integridad. |
| **R-09** | Medio | El producto no sería replicable, que es la meta declarada. | Ejemplos de plantilla siempre ficticios y genéricos; **B8-T06** prueba de agnosticidad con otro proyecto. |
| **R-10** | Medio | Vuelta al trabajo manual. | **B3-T02** exige cuestionario proporcional a la complejidad, no interrogatorio fijo. |

---

## 8. Validación contra Criterios de la Tarea (B0-T02)

* **Objetivo alcanzado:** Artefacto vivo de consulta ágil (`00-VISION.md`).
* **Inclusión de elementos obligatorios:** Contiene frase del producto, señal única, anti-objetivo, 5 criterios de éxito, principios P1 a P11, exclusiones y matriz de riesgos (R-01 a R-10).
* **Economía de contexto:** Toda mitigación redirige explícitamente a su tarea o principio controlador sin crear archivos redundantes (P4, P10 y P11).