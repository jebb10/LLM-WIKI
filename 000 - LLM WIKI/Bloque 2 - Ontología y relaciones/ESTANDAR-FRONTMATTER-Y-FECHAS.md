---
id_documento: ESTANDAR-FRONTMATTER-FECHAS-B2
tipo_documento: norma-tecnica
bloque: Bloque 2 - Ontología y relaciones
principios_aplicados:
  - P1
  - P4
  - P6
  - P10
  - P11
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-29
estado: Aprobado
---

# Estándar de Metadatos (YAML Frontmatter) y Formato de Fechas

Documento normativo técnico. Define la estructura obligatoria de **metadatos en bloque YAML (frontmatter)** para todos los archivos de la **LLM Wiki** y fija el estándar inmutable del formato de fechas.

* **Autor:** Johan Benítez — Product Owner / Líder de Requerimientos
* **Estado:** Aprobado

---

## 1. El Problema que Resuelve

Sin una estructura de metadatos estandarizada al inicio de cada archivo:
1. El agente debe **escanear todo el cuerpo de un documento** para conocer su tipo, estado o fecha, violando el **Principio P10** (*Economía de contexto*).
2. Los scripts de compilación y herramientas de búsqueda no pueden realizar filtrados rápidos por metadatos (ej. *"todos los requerimientos en estado En curso"*).
3. Las fechas escritas en formatos heterogéneos (ej: `25/07/26`, `Julio 25, 2026`, `2026-7-25`) impiden el ordenamiento alfabético y el cálculo automático de días transcurridos para stoppers y fechas límite.

---

## 2. Norma del Formato Estricto de Fechas

* **Formato Único e Inalterable:** **`AAAA-MM-DD`** (Año en 4 dígitos, Mes en 2 dígitos, Día en 2 dígitos, separados por guión).
* **Ejemplo Correcto:** `2026-07-26`
* **Formatos Prohibidos:** `26/07/2026`, `26-07-2026`, `2026/07/26`, `Julio 26 de 2026`.
* **Aplicabilidad:** Aplica a todo campo de fecha en el sistema: `fecha_creacion`, `fecha_actualizacion`, `fecha_corte`, `fecha_limite`, `fecha_real` y `fecha_origen` de stoppers.

---

## 2.1 Placeholder único de dato faltante

* **Formato único:** `[PENDIENTE]`, a secas — sin comillas, sin sufijo explicativo, sin variantes (ej. `[PENDIENTE — motivo]`). Aplica igual a cualquier campo de frontmatter o de cuerpo: dato que el PO aún no ha entregado, y valor de vocabulario cerrado a la espera de una decisión de gobierno.
* Si el motivo del vacío no es evidente por contexto, se explica en prosa junto al campo (fuera del propio placeholder), no dentro de su sintaxis.
* No se detiene la ficha completa por un campo en `[PENDIENTE]` — la sesión sigue sobre el resto del documento (ver `CLAUDE.md`).

---

## 3. Estructura Obligatoria de Metadatos (YAML Frontmatter)

Todo archivo `.md` creado dentro de la wiki debe iniciar en la **línea 1** con un bloque delimitado por tres guiones (`---`):

```yaml
---
id_documento: ID-UNICO-DOC
tipo_documento: norma | plantilla | requerimiento | seguimiento | historia-usuario | web-service | conclusion
bloque: Bloque N - Nombre del Bloque
principios_aplicados: [P1, P4, P6...]
fecha_creacion: AAAA-MM-DD
fecha_actualizacion: 2026-07-26
estado: Aprobado | En validacion | Pendiente | Deprecado
---
```

---

## 4. Esquemas Específicos por Tipo de Documento

### 4.1 Ficha de Requerimiento (Hoja Principal)
```yaml
---
id_documento: DEMO-REQ-001
tipo_documento: requerimiento
sigla_modulo: DEMO
naturaleza: Desarrollo
sponsor_po: Nombre del PO
estado_macro: En curso
fecha_recepcion: 2026-07-26
fecha_actualizacion: 2026-07-26
---
```

### 4.2 Documento Centralizador de Seguimiento
```yaml
---
id_documento: SEGUIMIENTO-DEMO-REQ-001
tipo_documento: seguimiento
id_requerimiento_padre: DEMO-REQ-001
fecha_corte_horas: 2026-07-26
horas_estimadas_total: 120.0
horas_consumidas_total: 45.0
stoppers_activos: 1
---
```

### 4.3 Ficha de Historia de Usuario (HU)
```yaml
---
id_documento: HU-DEMO-001
tipo_documento: historia-usuario
id_requerimiento_padre: DEMO-REQ-001
paso_flujo_id: P-01
actor: Empleado registrado
---
```

### 4.4 Ficha de Web Service (WS)
```yaml
---
id_documento: WS-DEMO-001
tipo_documento: web-service
id_canonical: WS-DEMO-001
id_proveedor: "EXT-1234"
nombre_tecnico: "WS_ConsultaDisponibilidad_V1"
alias: ["WS 1", "WS Disponibilidad"]
metodo_http: GET
url_qa: "https://qa.proveedor-externo.com/v1/disponibilidad"
sla: "3s"
estado_definicion: disponible
---
```

Vocabulario cerrado de `estado_definicion`: `pendiente-proveedor` · `en-contrato` · `disponible` · `deprecado`. Norma completa en `REGLA-IDENTIFICADOR-WS.md` §4.1.

---

## 5. Regla de Parsing para el Agente (Principio P10)

1. Al abrir cualquier documento de la wiki, el agente **lee únicamente las primeras 15 líneas** del bloque frontmatter para obtener el contexto completo del archivo.
2. Si el agente solo necesita saber el estado o la fecha de corte, **no lee el resto del documento**, ahorrando tokens y acelerando el tiempo de respuesta.
