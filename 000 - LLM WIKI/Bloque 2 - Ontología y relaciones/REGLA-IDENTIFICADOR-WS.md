---
id_documento: REGLA-IDENTIFICADOR-WS-B2
tipo_documento: norma-tecnica
bloque: Bloque 2 - Ontología y relaciones
principios_aplicados:
  - P1
  - P4
  - P6
  - P8
  - P10
  - P11
fecha_creacion: 2026-07-26
fecha_actualizacion: 2026-07-27
estado: Aprobado
---

# Regla del Identificador Estable de Web Service

Documento normativo de integración técnica. Define la regla de asignación de **ID Canónico e Inmutable** para todos los Web Services del proyecto, garantizando el desacoplamiento total entre las Historias de Usuario y los detalles de infraestructura o proveedores.

* **Autor:** Johan Benítez — Product Owner / Líder de Requerimientos
* **Estado:** Aprobado

---

## 1. El Problema que Resuelve

En proyectos de software reales, los proveedores modifican URLs, los métodos HTTP cambian (ej. de `POST` a `PUT`), los puertos se reasignan y las versiones de los servicios evolucionan (ej. `/v1/` a `/v2/`). 

Si las Historias de Usuario o Pasos de Flujo referencian un servicio por su URL o por nombres informales (ej. *"el WS 4"* o *"https://api.proveedor.com/v1/user"*), **cualquier cambio técnico obliga a actualizar manualmente decenas de documentos**, introduciendo desincronización y errores en el desarrollo.

---

## 2. La Regla del ID Canónico

1. **Unicidad e Inmutabilidad:**
   - Todo Web Service del proyecto recibe un ID Canónico con la sintaxis **`WS-[SIGLA]-[NNN]`** (ej. `WS-DEMO-001`).
   - El ID Canónico es **inmutable**: no cambia aunque el proveedor, la URL, la tecnología o la versión cambien.
2. **Prohibición de URLs Hardcodeadas:**
   - Queda estrictamente **prohibido incluir URLs (`http://...` / `https://...`)** en el cuerpo de las Historias de Usuario, Pasos de Flujo o Reglas de Negocio.
   - Las Historias de Usuario y Pasos de Flujo **únicamente referencian el ID Canónico** (ej. `[[ws-demo-001-consulta-disponibilidad-salas]]`).
3. **Resiliencia Técnicas:**
   - Ante cualquier cambio de URL, puerto, método HTTP o proveedor, **únicamente se actualiza la ficha individual del Web Service** (`ws-[sigla]-[nnn]-[nombre].md`).
   - Ninguna Historia de Usuario ni Paso de Flujo sufre modificaciones.

---

## 3. Manejo de Web Services "Por Definir"

Cuando durante las fases de Requerimiento o Diseño se identifique la necesidad de una integración cuya especificación técnica el proveedor no ha entregado:

1. Se crea la ficha del Web Service asignando su **ID Canónico** (ej. `WS-DEMO-008`).
2. Se establece su estado de definición con el vocabulario cerrado del §4.1.
3. Las Historias de Usuario y Pasos de Flujo referencian el ID `WS-DEMO-008`.
4. A medida que el proveedor entregue la especificación, el agente **actualiza esa misma ficha** hasta alcanzar el estado `disponible`, sin alterar las Historias de Usuario.

---

## 4. Esquema Estándar de Metadatos (YAML Frontmatter)

### 4.1 Vocabulario cerrado de estados de definición (B2-T06 — Cierra DP-23)

| Estado | Significa |
| :--- | :--- |
| `pendiente-proveedor` | El proveedor aún no ha entregado la especificación técnica del servicio. |
| `en-contrato` | La especificación llegó y está en validación/documentación (esta ficha se está completando). |
| `disponible` | El contrato está completo y verificado; el servicio puede consumirse. |
| `deprecado` | El servicio fue reemplazado o dado de baja; se conserva la ficha por trazabilidad histórica, no se referencia en HU nuevas. |

No se admiten variantes de redacción de estos 4 valores.

### 4.2 Esquema YAML obligatorio

Toda ficha de Web Service en la wiki debe iniciar obligatoriamente con el siguiente encabezado de metadatos:

```yaml
---
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

---

## 5. Mapeo de Alias y Traducción Automática

* **Múltiples Alias:** El campo `alias` almacena todos los nombres informales o históricos con los que el cliente o equipo se refiere al servicio.
* **Traducción en Ingesta:** Cuando el PO entregue una nota que mencione *"el servicio EXT-1234 cambió la respuesta"*, el agente resuelve el alias mediante los metadatos, actualiza únicamente la ficha `ws-demo-001-consulta-disponibilidad-salas.md` y registra la equivalencia en el log de ingesta.
