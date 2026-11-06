















## MANUAL DE DILIGENCIAMIENTO
## FORMATO HISTORIA DE USUARIO















Tabla de contenido


- Introducción y Propósito 3
## 2. Glosario 3
- Estructura del Documento 4
3.1. Identificación de la historia de usuario 4
3.2. Escenario de la HU 5
3.3. Reglas de negocio 6
3.4. Criterios de aceptación 7
## 3.5. Prototipos / Mockup 7
3.6.Flujo 8
3.7.Datos de entrada (input) y Datos de salida (output) 8
3.8.Notas 8
3.9.Anexos 9
## 3.10 Aprobadores 9

















- Introducción y Propósito
Este documento tiene como objetivo servir de guía completa para el correcto diligenciamiento del
formato "Especificación de Historias de Usuario". El documento está diseñado para estandarizar la
estructura en que los equipos funcionales identifican, describen, comunican y validan los
requerimientos de un proyecto.

## 2. Glosario
## Término Definición
Historia de Usuario (HU) Descripción breve de una funcionalidad desde la
perspectiva del usuario final. Expresada en
formato "Como [rol], quiero [objetivo], para
## [beneficio]".
Épica Agrupación de alto nivel que representa un
objetivo estratégico de negocio.
Feature Funcionalidad intermedia que agrupa varias
historias de usuario relacionadas.
Sprint Iteración de tiempo fijo (generalmente 2
semanas) en la que el equipo entrega
incrementos.
Criterio de Aceptación Condición verificable que define cuándo una
historia está completada.
Regla de Negocio Restricción o política del dominio que el sistema
debe cumplir obligatoriamente.
Product Owner (PO) Principal conocedor del negocio y responsable de
maximizar el valor del producto.
Refinamiento (Grooming) Sesión donde el equipo analiza, estima y
descompone historias del backlog.
Puntos de Historia Medida relativa de esfuerzo, complejidad e
incertidumbre de una historia.
Mockup / Prototipo Representación visual de la interfaz para
comunicar la idea de diseño.
Backlog Lista priorizada de historias de usuario
pendientes de desarrollo.
Pre-condiciones Son los requisitos o estados que deben cumplirse
antes de ejecutar una Historia de Usuario,
asegurando que el contexto necesario esté listo
para su correcto desarrollo y validación.


- Estructura del Documento
El formato contiene 9 secciones principales más un apartado de Anexos. A continuación se describe
cada sección en detalle, incluyendo su propósito, los campos que contiene y las instrucciones de
diligenciamiento.




3.1. Identificación de la historia de usuario
Esta sección contiene la metadata administrativa de la historia. Permite identificar, clasificar, priorizar
y rastrear la historia dentro del backlog.

Campo Descripción Instrucciones de
## Llenado
## Ejemplo
Id. Historia de Usuario Identificador único de
la historia dentro del
proyecto
Usar nomenclatura
estándar: prefijo +
número secuencial


## HU_SME_ADM_001_01
Id. Herramienta de
## Proyecto
Identificador en la
herramienta de gestión
(Jira, Azure DevOps)


Copiar el ID exacto que
genera
automáticamente la
herramienta utilizada

## 300914
Nombre Historia de
## Usuario
Título breve y
descriptivo de la
funcionalidad
Debe ser conciso
reflejando la acción
principal y ser
entendible por negocio


Registro de nuevo
cliente persona natural


## Épica / Feature
Agrupación jerárquica
superior a la que
pertenece la historia
Épica: objetivo
estratégico amplio.
Feature: funcionalidad
intermedia dentro de
la épica

Épica: Gestión de
usuarios
Feature: Crae usuarios
admin.

Prioridad Nivel de urgencia e
importancia de la
historia
## Seleccionar: Alta /
## Media / Baja
## Alta
Puntos de historia de
usuario
Estimación relativa del
esfuerzo usando la
escala del equipo
Usar escala Fibonacci
## (1, 2, 3, 5, 8, 13). Si
supera 13, considerar
dividir la HU

## 8


## Estado

Fase actual del ciclo de
vida de la historia

## Seleccionar: Pendiente
/ En análisis / En
desarrollo / QA /
## Cerrada

En análisis
Sprint Iteración en la que se
planifica desarrollar la
historia
Indicar número o
nombre del sprint
asignado
## Sprint 14
Fecha inicio Sprint Fecha en la que
comienza el sprint al
Registrar la fecha de
inicio del sprint en
formato
## 01/04/2026



cual se asigna la
historia de usuario
DD/MM/AAAA. Debe
coincidir con la fecha
oficial de inicio
definida en la
planificación del sprint.
Si la HU aún no esta
asignada a un sprint,
indicar "Por definir"
Dependencias HU Historias de usuario Listar las HU de las que
depende para cumplir
HU-003 (Módulo de
autenticación)
Pre-condiciones  Servicios o
componentes que
deben existir
previamente
Listar las
pre-condiciones de los
que depende. Si no hay
dependencias, indicar
"Ninguna". Muchas
dependencias = señal
de alerta
- El usuario debe estar
autenticado con sesión
activa
- El token JWT debe ser
válido y no estar
expirado
- El usuario debe
conocer su contraseña
actual


3.2. Escenario de la HU

Campo Pregunta Clave Instrucciones de
## Llenado
## Ejemplo



## Como (rol)
¿Quién es el usuario o
actor que necesita esta
funcionalidad?
Identificar el rol
específico (no usar
genéricos como
"usuario"). Debe ser un
rol reconocido en el
sistema o en el negocio


Como cliente persona
natural registrado



## Quiero (objetivo)
¿Qué acción o
funcionalidad necesita
realizar?
Describir la acción
concreta en verbo
infinitivo. Enfocarse en
el QUÉ, no en el CÓMO
técnico. (debe ser una
sola funcionalidad)

Quiero actualizar mis
datos de contacto
(teléfono y correo
electrónico)



## Para (beneficio)
¿Qué valor o beneficio
se obtiene al realizar
esta acción?
Expresar el beneficio
desde la perspectiva
del usuario o del
negocio. Debe ser un
resultado tangible y
medible cuando sea
posible

Para mantener mi
información
actualizada y recibir
notificaciones
correctamente




3.3. Reglas de negocio

Son restricciones, políticas o condiciones que el sistema debe cumplir obligatoriamente y que no son
negociables. No deben incluir detalles técnicos de implementación y deben ser máximo 10 reglas de
negocio.

## Columna Descripción Ejemplo
Regla de negocio (ID) Identificador de la
regla, con formato
secuencial.
## RN-01
## RN-02
## RN-03
Descripción Detalle claro y preciso
de la restricción o
política de negocio.
RN-01: El campo
correo electrónico
debe validar formato

## RFC 5322.
RN-02: El usuario
debe ser mayor de 18
años para completar el
registro.
RN-03: El monto
máximo por
transacción es de
## $5.000.000 COP.





3.4. Criterios de aceptación

Los criterios de aceptación definen las condiciones que deben cumplirse para considerar la historia
como completada.

## Columna Descripción Ejemplo
No. Número secuencial del
criterio
## 01
Dado que Contexto o estado
previo del sistema
antes de la acción
Completo todos los
campos obligatorios
correctamente
Cuando Acción o evento que
dispara el
comportamiento
Presiono “Guardar”
Entonces Resultado esperado
observable y verificable
La cuenta se crea y se
envía email de
bienvenida




Aspectos clave:
✔ Incluir escenarios positivos y negativos (errores, validaciones).
✔ Cubrir casos borde cuando sea relevante.
✔ Cada criterio debe ser independiente de los demás.
✔ Máximo 10,  si supera este número considerar dividir la HU.

## 3.5. Prototipos / Mockup

Espacio para incluir referencias visuales que complementen la descripción funcional de la historia.
Los prototipos ayudan a alinear la visión del equipo development y reducir ambigüedades.

Opciones de diligenciado:
i. Adjuntar enlaces a herramientas de prototipado (Figma, Adobe XD, Sketch, Balsamiq).
ii. Insertar capturas de pantalla o imágenes directamente en la celda.
iii. Si no se dispone de mockup, indicar "No aplica" o "Pendiente de diseño UX".

Ojo: Los prototipos son orientativos, no contractuales.






3.6.Flujo
Describe el proceso funcional que sigue el usuario para completar la acción descrita en la historia.

Opciones de diligenciado:
i. Describir el flujo paso a paso en lenguaje natural.
ii. Referenciar un diagrama BPMN, diagrama de actividades o diagrama de secuencia.
iii. Incluir flujo principal y flujos alternativos o de excepción.
iv. Puede complementarse con un enlace a la herramienta de diagramación

3.7.Datos de entrada (input) y Datos de salida (output)

## Columna Instrucciones
Nombre del campo Usar el nombre exacto del
campo en la UI o el nombre del
atributo en el modelo.
Tipo del campo Tipo de dato esperado:



## Ej: Texto, Numérico, Fecha,
Booleano, Lista desplegable,
Archivo, etc.
## Obligatoriedad Indicar: Obligatorio / Opcional.
Longitud Tipo de dato esperado:
Ej: Máx. 50 caracteres, 10
dígitos, Hasta 5 MB, etc.
Detalle del campo Incluir formato esperado:
Ej: Máscara, valores permitidos,
valor por defecto, etc.

3.8.Notas
Observaciones o consideraciones adicionales que no se encuentran contempladas en los campos
previamente definidos, pero que deben ser tenidas en cuenta de manera obligatoria para el
desarrollo de la historia de usuario, por ejemplo, los requerimientos no funcionales.









3.9.Anexos

Espacio para referenciar documentos externos que complementan la historia. (Solo si aplica)

## Columna Descripción
Tipo de documento Categoría del anexo: Documento técnico,
Manual, Normativa, etc.
Nombre del documento Título exacto del documento referenciado.
Página / Numeral Sección específica relevante dentro del
documento.
Ubicación del documento Ruta, URL o repositorio donde se encuentra.
Autor Creador del documento.
Fecha de envío Fecha en que se compartió o publicó.
Observación Notas adicionales sobre la relevancia del anexo.

## 3.10 Aprobadores
Sección de control y trazabilidad del documento. Registra quién creó, revisó y aprobó la historia, así
como el historial de cambios.



## Columna Descripción
Versión Número de versión del documento (V1,V2...)
Fecha Fecha de la versión en formato DD/MM/AAAA.
Autor Nombre de quien redactó o modificó la historia.
Revisado por Nombre del revisor técnico o funcional.
Aprobado por Nombre de quien aprueba formalmente (PO,
líder, etc).
Rol del aprobador Rol del aprobador dentro del equipo
Descripción de cambio Breve resumen de qué se modificó en esta
versión.
Estado Estado de la aprobación: Pendiente / En revisión
## Aprobado / Devuelto / Rechazado.

Observación: Tener en cuenta que los campos “Aprobado por” y “Rol” pueden variar dependiendo
del tipo de revisión realizada. Esta puede ser efectuada por el cliente o por un líder del equipo de
trabajo. Únicamente en los casos en que sea necesario, el agente podrá asumir el rol de aprobador
de la Historia de Usuario (HU).

