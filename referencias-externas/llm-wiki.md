---
id_documento: REFERENCIA-LLM-WIKI
tipo_documento: referencia-externa
fecha_creacion: 2026-07-28
fecha_actualizacion: 2026-07-28
estado: Aprobado
---

# Referencia externa — el patrón "LLM Wiki"

**Material de terceros. No es autoría de este proyecto.**

| Campo | Valor |
| :--- | :--- |
| **Título** | LLM Wiki |
| **Autor** | Andrej Karpathy |
| **Fuente** | https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f |
| **Consultado** | `2026-07-27` |

---

## Por qué está aquí

Este repositorio se inspira en ese patrón. La idea original que se retoma: en vez de que el LLM redescubra el conocimiento en cada consulta (como en un RAG clásico), el agente **construye y mantiene una wiki persistente** de archivos Markdown interconectados que se sitúa entre la persona y las fuentes crudas. Cada fuente nueva no se indexa para recuperarla después: se lee, se integra, y actualiza las páginas existentes, señalando dónde el dato nuevo contradice al viejo. El conocimiento se compila una vez y se mantiene vigente.

La analogía del autor: Obsidian es el IDE, el LLM es el programador, la wiki es el código.

---

## Qué aporta este proyecto sobre esa base

El patrón original es genérico y aplica a cualquier dominio (investigación, notas de un libro, seguimiento personal). Este repositorio lo lleva a un dominio concreto y le agrega lo que el patrón deja abierto:

- Un **modelo de entidades cerrado** de 5 niveles para proyectos de software (Requerimiento → Flujo → Paso → Historia de Usuario → Regla de Negocio, más Web Services).
- **Plantillas normativas** por tipo de documento, con vocabularios cerrados y frontmatter obligatorio.
- **11 principios rectores** que restringen el comportamiento del agente, en particular: nunca resuelve una contradicción por su cuenta.
- **6 subagentes de auditoría** que vigilan la integridad de la propia bóveda (enlaces, estructura, forma del grafo, consistencia interna).

---

**Nota de uso:** esta página describe y acredita la fuente; no reproduce su texto. Para leer el original completo, ver el enlace de la tabla de arriba.
