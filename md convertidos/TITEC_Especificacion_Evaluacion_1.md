TITEC – Especificación Evaluación 1

Taller de Integración Tecnológica · 2026-2

# 1. Descripción general y cálculo de notas

La Evaluación 1 de Taller de Integración Tecnológica vale 15% del curso y se compone de dos partes que usan la misma rúbrica: la entrega del proyecto en GitHub y la presentación del producto.

| **Componente** | **Ponderación en el curso** | **Cómo se evalúa** |
| --- | --- | --- |
| Entrega del proyecto en GitHub | 10% | Inspección detallada del repositorio en su estado al cierre de la entrega |
| Presentación del producto | 5% | Lo que el equipo muestra en vivo durante la reunión asignada |

## Nota por rol

La rúbrica agrupa sus 16 ítems en cinco roles: Back End, Base de Datos, UI/UX (front end), Gestión y Calidad. Cada ítem se califica con 4 (Logrado), 2 (Medianamente logrado), 1 (No logrado) o 0 (No observado). La nota de cada rol es el promedio de sus ítems, convertido a la escala 1,0–7,0.

## Nota grupal e individual

* **Nota grupal:** promedio simple de las cinco notas por rol.
* **Nota individual:** 50% la nota del rol o roles de los que la persona es responsable, y 50% la nota grupal.

*Nota individual = 0,5 × Nota de su(s) rol(es) + 0,5 × Nota grupal*

Este cálculo se hace por separado para la entrega en GitHub y para la presentación. Cada estudiante obtiene así dos notas individuales, que pesan 10% y 5% del curso.

# 2. Asignación de responsables

Cada equipo debe declarar qué integrante o integrantes son responsables de cada rol. El responsable de un rol responde por todos los ítems de la rúbrica asociados a ese rol, y esa nota de rol es la que compone su parte individual.

* Cada rol debe tener al menos un responsable.
* Cada integrante debe ser responsable de al menos un rol.
* Una persona puede estar a cargo de más de un rol; su parte individual será el promedio de las notas de esos roles.
* La tabla debe estar en el repositorio (por ejemplo, en el README o en un archivo RESPONSABLES.md en la raíz) antes del cierre de la entrega. Se usará la versión vigente a esa hora.

Formato sugerido:

| **Rol** | **Ítems de la rúbrica** | **Responsable(s)** |
| --- | --- | --- |
| Back End | BE1, BE2, BE3 |  |
| Base de Datos | BD1, BD2, BD3, BD4 |  |
| UI/UX (front end) | UI1, UI2, UI3 |  |
| Gestión | GE1, GE2, GE3, GE4 |  |
| Calidad | CA1, CA2 |  |

# 3. Componente 1: entrega del proyecto en GitHub (10%)

Todos los equipos entregan el **miércoles 30 de septiembre de 2026 a las 14:30**. No se revisarán cambios posteriores a esa hora.

* **Código de la aplicación:** en primer lugar, el repositorio debe contener el código fuente de la aplicación (back end, front end y scripts de base de datos). Sin código, el resto de las evidencias no es evaluable.
* **Qué se evalúa:** los mismos 16 ítems de la rúbrica (sección 6).
* **Cómo se evalúa:** en la presentación se hace una revisión preliminar; luego cada ítem se evalúa en detalle inspeccionando el repositorio.
* **Estado evaluado:** el repositorio tal como quedó a las 14:30. Commits, cambios en issues o tableros y archivos agregados después de esa hora no se consideran.
* **Otras evidencias esperadas:** Swagger de servicios propios y de servicios requeridos por otros módulos; código de invocación a servicios externos; diagrama relacional y script de creación con diccionario de datos; planificación, historias de usuario y avance en GitHub (issues, proyecto o equivalente); evidencias de pruebas de funcionalidad; colección Postman o similar con casos de prueba de integración; tabla de responsables por rol.
* **Sin evidencia:** un ítem sin evidencia en el repositorio se califica como No observado (0 puntos).

# 4. Componente 2: presentación del producto (5%)

Cada equipo presenta en su horario asignado, con todo el grupo presente, en un máximo de 10 minutos más 5 minutos de preguntas.

## Reglas

* **Participación:** debe estar todo el grupo. Presenta el Scrum Master; otros integrantes pueden intervenir, pero el tiempo total no se extiende.
* **Tiempo:** 10 minutos como máximo para presentar antecedentes. Al minuto 10 se termina la presentación, aunque no se haya mostrado todo. La presentación debe venir preparada.
* **Preguntas:** hasta 5 minutos de preguntas del profesor para aclarar elementos. No es tiempo para mostrar evidencias nuevas.
* **Aplicación funcionando:** es requisito para presentar. Puede ejecutarse en modo local.
* **Lo que no se muestra vale 0:** todo ítem que no se muestre durante la presentación se califica con 0 en este componente, aunque esté disponible en el repositorio. El repositorio se evalúa aparte en el componente 1.

## Estructura sugerida

1. Producto funcional (UI/UX): recorrer las historias de usuario finalizadas en la aplicación.
2. Back End: Swagger de servicios propios y de servicios requeridos por otros módulos; código de invocación a servicios externos.
3. Base de Datos: diagrama relacional generado desde la base de datos del proyecto y diccionario de datos.
4. Gestión: sprints, historias con responsables, criterios de aceptación, definition of done, política de autorización, avance e ítems de integración en GitHub.
5. Calidad: evidencias de pruebas de funcionalidad y colección de pruebas de integración.

## Horarios

| **Equipo** | **Día** | **Hora** | **Profesor** |
| --- | --- | --- | --- |
| Auth | Miércoles 30 sep | 14:40 | R. Alfaro |
| Panel organizador | Miércoles 30 sep | 15:00 | R. Alfaro |
| Catálogo de eventos | Miércoles 30 sep | 15:20 | R. Alfaro |
| Entradas/inventario | Miércoles 30 sep | 16:20 | R. Noël |
| Pagos | Miércoles 30 sep | 16:40 | R. Noël |
| Check-in | Miércoles 30 sep | 17:00 | R. Noël |
| Reseñas | Jueves 1 oct | 08:40 | Sh. Torres |
| Notificaciones | Jueves 1 oct | 09:00 | Sh. Torres |
| Promociones | Jueves 1 oct | 09:20 | Sh. Torres |

# 5. Dependencias de datos entre módulos

La tabla de dependencias TITEC 2026-2 se entrega como referencia. En esta entrega se evalúa la definición de los servicios de integración, no las integraciones efectivamente logradas. Los servicios de Back End y el diseño de la base de datos deben ser consistentes con la tabla; los ítems BE2, BE3, BD1, BD2 y GE4 se revisan contra ella.

## Reglas de consistencia

* **Datos que genero:** son los datos de negocio propios del módulo. Deben estar en su base de datos y considerados en su Swagger cuando otro módulo los necesita.
* **Datos que envío:** cada envío implica al menos un servicio propio definido en Swagger que otro módulo consumirá (ítem BE3).
* **Datos que recibo:** cada recepción implica definir la invocación a un servicio del módulo de origen (ítem BE2). Basta con la definición; no se exige que la integración funcione en esta entrega. Esos datos no se replican como tablas de negocio propias; solo se guardan identificadores de referencia, por ejemplo id usuario o id evento (ítem BD2).
* **Integración planificada:** toda dependencia debe tener un ítem de trabajo en GitHub (ítem GE4).

## Tabla de dependencias

| **Módulo** | **Datos que genera** | **Datos que envía (a quién)** | **Datos que recibe (de quién)** |
| --- | --- | --- | --- |
| Auth | id token; nombre, rut y correo de usuario; contraseña; versión token; url temporal de recuperación; usuario (id, rol) | id token, rol usuario y usuario (id, rol) (Catálogo); correo usuario y url temporal de recuperación (Notificaciones) | Confirmación (Notificaciones); rol usuario (Panel) |
| Catálogo de eventos | — | — | Promedio de calificaciones (Reseñas); nombre, horario, fecha, dirección y descripción del evento (Panel) |
| Entradas/inventario | Estado entrada; cantidad de entradas reservadas y compradas; máximo de tickets; stock actual; id entrada; QR | id usuario (Notificaciones, Promociones); nombre, hora y fecha del evento y cantidad de entradas (Notificaciones); QR y nombre usuario (Check-in); cantidad de entradas compradas (Promociones) | id usuario, nombre, hora y fecha del evento, cantidad de entradas y tipo de entrada pago/gratis (Panel); porcentaje de descuento e id evento (Promociones); id pago (Pagos); nombre usuario (Auth) |
| Pagos | Estado del pago; id pago | Fecha de creación de la compra y estado del pago (Entradas); id pago (Entradas, Promociones) | Orden de compra: cantidad de entradas y total (Entradas) |
| Check-in | Lista de asistencia (id evento, usuario); hora de llegada | id evento, nombre usuario y usuario (id, rol) (Reseñas) | Usuario (id, rol) (Auth); id ticket y nombre usuario (Entradas); id, nombre, dirección, hora de inicio, hora de fin y fecha del evento (Panel) |
| Reseñas | Promedio de calificaciones; texto de reseña; puntuación por reseña | Promedio de calificaciones (Catálogo) | id y nombre del evento (Catálogo); nombre usuario y usuario (id, rol) (Check-in) |
| Panel organizador | Nombre, horario, fecha, dirección y descripción del evento; cantidad de entradas; tipo de entrada; imagen; nuevo estado; fecha de cambio | Nombre, horario, fecha, dirección y descripción del evento (Catálogo); usuario (id, rol) (Auth, por confirmar) | id token (Auth); usuario (id, rol) (Auth, por confirmar) |
| Notificaciones | Nombre de notificación; hora y fecha de creación; estado leído/no leído | Confirmación (Auth, Panel) | Correo usuario y url temporal de recuperación (Auth); nombre, hora y fecha del evento, cantidad de entradas y usuario (id, rol) (Entradas); id evento, nuevo estado y fecha de cambio (Panel) |
| Promociones | Porcentaje de descuento; fechas de inicio y fin del descuento; cantidad de códigos; nombre del código | Porcentaje de descuento e id evento (Entradas) | id evento (Panel); usuario (id, rol) (Auth); cantidad de entradas (Entradas); id pago (Pagos); precio (Catálogo) |

La tabla tiene algunas asimetrías entre lo que un módulo envía y lo que otro declara recibir (por ejemplo, Catálogo no declara envíos, pero Reseñas y Promociones reciben datos de Catálogo). Los equipos involucrados deben acordarlas y reflejar el acuerdo en sus Swagger.

# 6. Rúbrica

Cada ítem se califica en cuatro niveles: Logrado (4), Medianamente logrado (2), No logrado (1) y No observado (0). En los descriptores, "la mayoría" significa más de la mitad y "una parte menor", la mitad o menos. En la presentación, No observado corresponde a un ítem que no se mostró; en GitHub, a un ítem sin evidencia en el repositorio.

## Back End

| **Ítem y medio de verificación** | **Logrado (4)** | **Medianamente logrado (2)** | **No logrado (1)** | **No observado (0)** |
| --- | --- | --- | --- | --- |
| BE1. Servicios propios. Verificación: Swagger de servicios propios del módulo | Define los servicios necesarios para soportar la lógica de negocio descrita en las historias de usuario | Define servicios para la mayoría de las historias, pero faltan algunos o su definición está incompleta (rutas, parámetros, respuestas o errores sin especificar) | Define servicios para una parte menor de las historias, o los servicios no corresponden a la lógica de negocio descrita | No se presenta Swagger de servicios propios |
| BE2. Servicios que requiere de otros squads. Verificación: código de invocación de servicio externo (se evalúa la definición, no si la integración funciona) | Define todos los servicios que requiere de otros squads | Define la invocación de la mayoría de los servicios externos que requiere según la tabla de dependencias, o la definición de algunas invocaciones está incompleta | Define la invocación de una parte menor de los servicios requeridos, o las invocaciones no corresponden a la tabla de dependencias | No se presenta código de invocación a servicios externos |
| BE3. Servicios que requieren otros squads. Verificación: Swagger de servicios requeridos por otros módulos (al menos 1) | Define todos los servicios que requieren otros squads | Documenta en Swagger la mayoría de los servicios que otros módulos requieren según la tabla de dependencias, o su documentación está incompleta | Documenta una parte menor de esos servicios, o documenta servicios que no corresponden a lo que otros módulos requieren | No se presenta Swagger de servicios para otros módulos |

## Base de Datos

| **Ítem y medio de verificación** | **Logrado (4)** | **Medianamente logrado (2)** | **No logrado (1)** | **No observado (0)** |
| --- | --- | --- | --- | --- |
| BD1. Soporte a historias de usuario. Verificación: diagrama relacional desde la base de datos del proyecto | Permite soportar la funcionalidad de las historias de usuario | Soporta la mayoría de las historias; faltan entidades o atributos para algunas | Soporta una parte menor de las historias, o faltan entidades centrales del módulo | No se muestra diagrama relacional generado desde la base de datos |
| BD2. Sin datos de negocio de otros squads. Verificación: diagrama relacional desde la base de datos del proyecto | No incluye datos de negocio de otros squads en su diseño | Replica algunos atributos de negocio de otros squads, además de los identificadores de referencia | Replica entidades completas que pertenecen a otros squads | No se muestra diagrama relacional generado desde la base de datos |
| BD3. Nomenclatura y documentación. Verificación: diagrama relacional; diccionario de datos (script de creación) | Respeta los estándares de nomenclatura acordados; todas las tablas y atributos están documentados | Respeta la nomenclatura en la mayoría de las tablas y atributos, o la documentación está incompleta | Nomenclatura inconsistente en gran parte del diseño, o documentación de una parte menor de tablas y atributos | No se muestra diagrama ni diccionario de datos |
| BD4. Diseño técnico. Verificación: diagrama relacional desde la base de datos del proyecto | Diseño técnico correcto: llaves primarias, tipos de datos, llaves foráneas, nulabilidad y sin ciclos en las relaciones | Errores puntuales que no comprometen la integridad (por ejemplo, algún tipo de dato inadecuado o nulabilidad mal definida) | Errores estructurales: tablas sin llave primaria, relaciones sin llave foránea o ciclos en las relaciones | No se muestra diagrama relacional generado desde la base de datos |

## UI/UX (front end)

| **Ítem y medio de verificación** | **Logrado (4)** | **Medianamente logrado (2)** | **No logrado (1)** | **No observado (0)** |
| --- | --- | --- | --- | --- |
| UI1. Soporte a historias finalizadas. Verificación: aplicación funcional | Permite soportar la funcionalidad de las historias de usuario finalizadas | Soporta la mayoría de las historias finalizadas; algunos flujos están incompletos o con errores | Soporta una parte menor de las historias finalizadas, o la aplicación falla en flujos principales | No se muestra la aplicación funcionando |
| UI2. Información para la tarea. Verificación: aplicación funcional | Las interfaces muestran y gestionan toda la información necesaria para realizar la tarea | La mayoría de las interfaces muestran y gestionan la información necesaria; en algunas faltan datos, acciones, validaciones o mensajes | En la mayoría de las interfaces faltan datos o acciones esenciales para realizar la tarea | No se muestra la aplicación funcionando |
| UI3. Estándares de UI. Verificación: aplicación funcional | Respeta los estándares de UI acordados con otros módulos | Respeta la mayoría de los estándares, con desviaciones puntuales (colores, tipografía, componentes o navegación) | Respeta una parte menor de los estándares acordados | No se muestra la aplicación funcionando |

## Gestión

| **Ítem y medio de verificación** | **Logrado (4)** | **Medianamente logrado (2)** | **No logrado (1)** | **No observado (0)** |
| --- | --- | --- | --- | --- |
| GE1. Planificación. Verificación: GitHub | Planificación de sprints, historias y responsables asignados por historia | Sprints planificados, pero parte de las historias no tiene sprint o responsable asignado | Planificación mínima: sprints sin historias asociadas, o la mayoría de las historias sin responsable | No hay evidencia de planificación en GitHub |
| GE2. Documentación de historias. Verificación: GitHub | Historias con descripción, criterios de aceptación, definition of done y política de seguridad (autorización) | La mayoría de las historias tiene descripción y criterios de aceptación, pero falta definition of done o política de seguridad en algunas | Las historias tienen solo título o descripción, sin criterios de aceptación en la mayoría | No hay historias de usuario documentadas en GitHub |
| GE3. Avance actualizado. Verificación: GitHub | Avance actualizado según los resultados del proyecto | El avance está parcialmente actualizado; algunos estados no reflejan lo realmente logrado | El avance está mayormente desactualizado respecto de lo realmente logrado | No hay registro de avance en GitHub |
| GE4. Trabajo de integración. Verificación: GitHub | Considera ítems de trabajo de integración con otros módulos | Considera ítems de integración para la mayoría de las dependencias de la tabla | Considera ítems de integración para una parte menor de las dependencias, o solo de forma genérica | No hay ítems de integración en GitHub |

## Calidad

| **Ítem y medio de verificación** | **Logrado (4)** | **Medianamente logrado (2)** | **No logrado (1)** | **No observado (0)** |
| --- | --- | --- | --- | --- |
| CA1. Pruebas de funcionalidad. Verificación: según tecnología del proyecto, en GitHub | Existe evidencia de pruebas de funcionalidad | Hay pruebas para la mayoría de las funcionalidades implementadas, o no hay evidencia de su ejecución y resultados | Hay pruebas para una parte menor de las funcionalidades, o son triviales y no validan comportamiento | No hay evidencia de pruebas de funcionalidad |
| CA2. Pruebas de integración. Verificación: Postman o similar con casos de prueba | Existe evidencia de pruebas de integración | Hay casos de prueba para la mayoría de los servicios de integración, o les falta el resultado esperado | Hay solicitudes aisladas sin casos de prueba definidos | No hay evidencia de pruebas de integración |