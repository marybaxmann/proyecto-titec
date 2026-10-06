**Contrato de interfaz: Panel organizador ↔ Check-in**

Versión: 1.0 (borrador para revisión)

| **Campo** | **Detalle** |
| --- | --- |
| Equipo consumidor | Check-in |
| Equipo proveedor | Panel organizador |
| Operación | consultar\_evento (Check-in → Panel organizador). |
| Basado en | Matriz de dependencia de datos (TITECT 2026-2), proceso de validación de entradas mediante QR y presentación del proyecto TicketU (REST detrás del API Gateway, contratos OpenAPI). |
| Nomenclatura | Los atributos siguen el formato atributo\_categoría (ej. id\_evento, nombre\_evento, fecha\_evento). |

# 1. Propósito

El microservicio de Check-in necesita conocer los datos del evento al que pertenece una entrada cuando el staff valida el ingreso de asistentes: nombre, dirección, fecha y horario. Estos datos son creados y administrados por el equipo de Panel organizador, por lo que Check-in no accede directamente a su base de datos.

Check-in realiza una solicitud al servicio de Panel organizador utilizando el identificador del evento (id\_evento) y recibe la información necesaria para mostrarla al staff y para verificar que la entrada corresponde al evento en curso.

Como Panel organizador administra eventos y no entradas, no puede interpretar el contenido de un código QR. Por eso la sección 3 propone cómo Check-in obtiene el id\_evento a partir de lo que se lee al escanear el QR.

# 2. Operación: Consultar información de evento (consultar\_evento)

## 2.1 Descripción

Permite a Check-in consultar los datos de un evento a partir de su identificador único (id\_evento). Se ejecuta después de que Check-in identificó a qué evento pertenece la entrada escaneada (ver sección 3).

## 2.2 Quién la expone

Equipo Panel organizador.

## 2.3 Quién la consume

Equipo Check-in.

## 2.4 Endpoint propuesto

GET /api/v1/panel/eventos/{id\_evento}

El endpoint indicado corresponde a una propuesta inicial y queda sujeto a confirmación con el equipo de Panel organizador.

## 2.5 Request (lo que se envía)

| **Campo** | **Tipo** | **Obligatorio** | **Descripción** |
| --- | --- | --- | --- |
| id\_evento | string | Sí | Identificador único del evento, obtenido a partir de la entrada escaneada (ver sección 3). |

Ejemplo:

GET /api/v1/panel/eventos/evt-77889

## 2.6 Response (lo que se recibe)

| **Campo** | **Tipo** | **Obligatorio** | **Descripción** |
| --- | --- | --- | --- |
| id\_evento | string | Sí | Identificador único del evento. |
| nombre\_evento | string | Sí | Nombre del evento. |
| direccion\_evento | string | Sí | Dirección o lugar donde se realiza el evento. |
| fecha\_evento | string | Sí | Fecha del evento en formato AAAA-MM-DD. |
| hora\_inicio\_evento | string | Sí | Hora de inicio en formato HH:mm (24 horas). |
| hora\_fin\_evento | string | Sí | Hora de término en formato HH:mm (24 horas). |

Ejemplo:

{

"id\_evento": "evt-77889",

"nombre\_evento": "Fiesta de generación 2026",

"direccion\_evento": "Gimnasio Central, Campus Principal",

"fecha\_evento": "2026-11-14",

"hora\_inicio\_evento": "21:00",

"hora\_fin\_evento": "03:00"

}

## 2.7 Códigos de error

| **Código** | **Significado** |
| --- | --- |
| 400 | Solicitud incompleta o id\_evento con formato inválido. |
| 401 | Sesión del staff ausente, inválida, expirada o revocada (según la validación con Auth). |
| 403 | El rol del usuario no está autorizado para consultar datos de eventos. |
| 404 | El evento asociado al id\_evento no existe. |
| 500 | Error interno del servicio de Panel organizador. |
| 503 | Servicio de Panel organizador temporalmente no disponible. |

## 2.8 Tiempo de respuesta esperado (SLA)

Pendiente a acordar entre ambos equipos. El tiempo de respuesta debe ser compatible con el requisito de Check-in de entregar el resultado de la lectura dentro del tiempo máximo establecido para evitar filas en el acceso.

# 3. Origen del id\_evento a partir del QR (propuesta)

El dato que entrega el QR al escanearlo aún no está definido: en el contrato de Entradas / Inventario ↔ Check-in es un pendiente (campo qr\_entrada). Panel organizador solo entiende id\_evento, de modo que Check-in necesita obtener ese identificador a partir de lo que lee el QR. Se proponen dos alternativas y se recomienda la A.

| **Opción** | **Qué codifica el QR** | **Ventajas** | **Desventajas** |
| --- | --- | --- | --- |
| A (recomendada) | Un identificador o token de la entrada (id\_entrada o un valor derivado de ella). | El id\_evento sale de los datos registrados por Entradas, no del QR, así que no se puede alterar modificando el código. El QR queda corto y fácil de leer. | Requiere que la entrada esté registrada en Check-in, o consultar a Entradas / Inventario si no lo está. |
| B | id\_entrada junto con id\_evento dentro del mismo valor (idealmente firmado). | Check-in podría consultar a Panel sin buscar antes la entrada. | El id\_evento del QR no es confiable si no va firmado. Mezcla datos de dos servicios en el QR y hace más difícil cambiar el formato. |

Flujo propuesto con la opción A:

1. El staff escanea el QR y Check-in obtiene el valor de qr\_entrada.
2. Check-in busca la entrada en su registro local, cargado con la operación enviar\_qr\_generado, que incluye id\_entrada e id\_evento. Si no la encuentra, la consulta a Entradas / Inventario con consultar\_entrada, cuya respuesta también incluye id\_evento.
3. Check-in compara el id\_evento de la entrada con el evento en curso del staff; si no coinciden, la entrada no corresponde a este evento.
4. Check-in consulta a Panel organizador con consultar\_evento usando ese id\_evento y obtiene los datos del evento.
5. Check-in usa esos datos para mostrarlos al staff y para verificar la fecha y el horario del evento; la decisión de aceptar la entrada es de Check-in.

# 4. Reglas de uso

1. Check-in debe consultar utilizando un id\_evento obtenido a partir de la entrada validada, y no uno tomado directamente de un dato sin verificar.

2. Check-in no debe acceder directamente a la base de datos de Panel organizador.

3. Panel organizador debe responder con los datos definidos en este contrato cuando el evento exista, o con el código de error correspondiente cuando no exista.

4. Check-in debe extraer únicamente los campos que necesita y no debe modificar los datos del evento.

5. La información entregada por Panel organizador no implica que ese equipo decida si una entrada se acepta; esa decisión corresponde a Check-in.

6. Los nombres de atributos deben respetar la nomenclatura atributo\_categoría y los identificadores se tratan como string.

7. Panel organizador debe publicar la especificación OpenAPI de la operación que expone antes de integrarse, y las llamadas se realizan a través del API Gateway.

# 5. Versionado y cambios

Cualquier actualización en los datos compartidos, la estructura del request o del response, el mecanismo de comunicación o el dato que codifica el QR requerirá revisión y acuerdo entre ambos equipos.

Los cambios que rompan la compatibilidad deberán utilizar una nueva versión del contrato.

# 6. Dueños del contrato

| **Rol** | **Equipo** | **Contacto** |
| --- | --- | --- |
| Dueño del contrato | Panel organizador | [Representante de Panel organizador] |
| Proveedor de la información de eventos | Panel organizador | [Representante de Panel organizador] |
| Consumidor principal | Check-in | [Representante de Check-in] |

# 7. Pendientes a acordar

## Origen del identificador

**☐** Definir qué dato codifica el QR (opción A o B de la sección 3). Debe acordarse en conjunto con Entradas / Inventario, que es quien genera el QR.

**☐** Definir cómo conoce Check-in el evento en curso del staff: selección manual en la app o asignación desde Panel organizador.

**☐** Confirmar que Panel organizador expone id\_evento: la matriz lo lista como dato que Check-in recibe, pero no aparece entre los datos que Panel genera.

## Datos

**☐** Confirmar que Panel organizador entrega hora de inicio y hora de término por separado. La matriz de Panel lista un único campo "horario".

**☐** Confirmar el nombre y formato definitivo de cada campo (id\_evento, nombre\_evento, direccion\_evento, fecha\_evento, hora\_inicio\_evento, hora\_fin\_evento) y la zona horaria de fecha y horas.

**☐** Definir cómo se representa un evento que termina después de medianoche, como en el ejemplo (inicio 21:00, término 03:00).

**☐** Confirmar si Check-in necesita también el estado del evento (por ejemplo, cancelado o modificado) para rechazar entradas de eventos que ya no se realizan.

## Comunicación y seguridad

**☐** Confirmar el nombre definitivo de la operación y del endpoint.

**☐** Confirmar el mecanismo de autenticación y autorización entre microservicios. Propuesta: Check-in reenvía la cookie de sesión del staff, Panel organizador valida la sesión con Auth (GET /internal/validar-sesion) y autoriza solo los roles staff y organizador.

**☐** Confirmar los códigos de error y la estructura de la respuesta de error.

**☐** Confirmar el SLA de la consulta.

**☐** Definir si Check-in puede guardar temporalmente los datos del evento para no consultar en cada escaneo, cómo se actualizan si el evento cambia y qué hace Check-in si Panel organizador no está disponible.

**Nota:** Los elementos indicados en el apartado “Pendientes a acordar” no se consideran definiciones definitivas del contrato hasta que sean revisados y aceptados por Panel organizador y Check-in.