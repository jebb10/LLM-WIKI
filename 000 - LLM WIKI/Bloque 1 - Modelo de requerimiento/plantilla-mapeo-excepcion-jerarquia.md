---
id_documento: PLANTILLA-MAPEO-EXCEPCION-B1
tipo_documento: plantilla
bloque: Bloque 1 - Modelo de requerimiento
def_cerradas: []
principios_aplicados:
  - P1
  - P4
  - P8
  - P9
  - P10
  - P11
fecha_creacion: 2026-07-27
fecha_actualizacion: 2026-07-27
estado: Aprobado
---

# Mapeo de Excepción de Jerarquía — [SIGLA]-REQ-[NNN]

Documento asociado para un requerimiento cuya fuente original no sigue la jerarquía canónica de 5 niveles (Requerimiento → Flujo → Paso de Flujo → Historia de Usuario → Regla de Negocio). Existe porque **la fuente original nunca se modifica** (P9) — este documento traduce su estructura real hacia el modelo, sin tocar el original.

**Cuándo se usa:** solo cuando el PO confirma explícitamente que un requerimiento es una excepción (ver DEC-59 para el caso de origen, ej. `DEMO-REQ-001`). No se crea de forma preventiva para requerimientos que sí encajan en la jerarquía estándar.

---

## 1. Identificación

| Campo | Valor |
| :--- | :--- |
| **Requerimiento** | `[SIGLA]-REQ-[NNN]` |
| **Fuente original (inmutable)** | `[Documento o plan de origen — nunca se edita]` |
| **Estructura nativa de la fuente** | `[Ej. Epic → Feature → HU técnica → Tarea]` |
| **Decisión que autoriza la excepción** | `[DEC-NN]` |

---

## 2. Tabla de equivalencia

Traduce cada nivel de la fuente nativa a su elemento canónico más cercano, sin forzar el ajuste si no existe equivalente real.

| Estructura nativa | Elemento canónico equivalente | Nota |
| :--- | :--- | :--- |
| `[Nivel nativo 1]` | `[Requerimiento / Flujo / HU / RN / —]` | `[Aclaración si la equivalencia no es 1:1]` |

---

## 3. Qué no se traduce

`[Elementos de la fuente nativa sin equivalente canónico — quedan documentados solo aquí, sin forzar el modelo. Si todo tiene equivalente, se omite esta sección.]`

---

## 4. Reglas de uso

1. **Este documento nunca reemplaza ni edita la fuente original** (P9). Solo traduce.
2. Se actualiza cuando cambia el mapeo, no cuando cambia el contenido de la fuente — eso se refleja en el documento de Seguimiento del requerimiento.
3. **Las secciones vacías se omiten** (P11).
