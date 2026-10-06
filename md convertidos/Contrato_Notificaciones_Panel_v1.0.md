Contrato de interfaz: Panel Organizador ↔ Notificaciones

Versión: 1.0

Equipo consumidor:  Notificaciones

Equipo proveedor: Panel Organizador

Basado en: HU6 — Recibir notificación por cancelación o cambios de evento

1. Propósito
Notificaciones necesita conocer los cambios relevantes en el estado de un evento
(modificaciones y cancelaciones) para informar oportunamente a los usuarios que poseen
entradas activas. Panel Organizador publica un evento cuando un organizador cancela o
modifica el estado de un evento.

2. Operación: Publicar evento evento_actualizado

2.1 Descripción

Publica un evento cuando el estado de un evento cambia y los asistentes deben ser
informados.

2.2 Quién la expone

Equipo Panel Organizador.

2.3 Quién la consume

Equipo Notificaciones, en el momento en que el organizador realiza una cancelación o cambio
que debe ser comunicado a los asistentes.

2.4 Endpoint propuesto
[EVENTO ASÍNCRONO] panel.evento.actualizado

(Comunicación vía broker de mensajes asíncrono).

2.5 Request (lo que se envía)
Campo

Tipo

tipo

string

Id_evento

integer

nuevo_estado

string

Sí

Sí

Sí

fecha_cambio

datetime

No

Ejemplo:

Obligatorio

Descripción

Tipo de evento. Debe ser
evento_actualizado.

Identificador del evento modificado.

Nuevo estado del evento: borrador,
cancelado, finalizado y reprogramado.

Fecha y hora en que se realizó el cambio del
evento (en el caso que sea reprogramado)

{
  "tipo": "evento_actualizado",
  "evento_id": 45,

   "nuevo_estado": "reprogramado",

   "fecha_cambio": "2026-09-13T:20:00:00",
}

2.6 Response (lo que se recibe)
Campo

Tipo

Obligatorio  Descripción

Id_evento

estado_envio

integer

Sí

Identificador del evento afectado.

Resultado del proceso de envío. Puede
ser exitoso o error.

Cantidad de usuarios a los que se envió
la notificación correctamente.

Cantidad de usuarios a los que se les
puedo enviar la notificación
correctamente.

Fecha y hora en que finalizó el proceso
de envío.

Mensaje informativo sobre el resultado
del envió.

usuarios_notificados

integer

Usuarios_faltantes

integer

fecha_envio

datetime

mensaje

string

Ejemplo:

{
  "id_evento": 45,

  "estado_envio": "exitoso",

  "usuarios_notificados": 155,

  "usuarios_faltantes": 0,

  "fecha_envio": "2026-09-13T:20:00:00",

  "mensaje": "Envió realizado correctamente"
}

Nota de diseño: Panel Organizador no necesita enviar a Notificaciones la lista de
usuarios asistentes. Notificaciones obtiene los usuarios que poseen entradas activas
para el evento_id recibido.

2.7 Códigos de error

Al tratarse de comunicación asíncrona, no se utilizan códigos HTTP para la respuesta del
evento.

Los errores de procesamiento o envío serán registrados por Notificaciones. El envío tendrá
hasta 3 intentos antes de registrar el error correspondiente.

2.8 Tiempo de respuesta esperado (SLA)

El evento debe ser publicado inmediatamente después de la emisión de las entradas, ≤ 5
segundos.

3. Reglas de uso (lado consumidor)

1.  Notificaciones permanece suscrito al evento evento_actualizado mediante el broker.

2.  Al recibirlo, identifica el evento mediante evento_id y obtiene los usuarios que poseen

entradas activas.

3.  Genera y almacena una notificación para cada usuario afectado.

4.  Envía las notificaciones y realiza hasta 3 intentos en caso de error.

5.  Una vez realizado el proceso, se informa al organizador que “El envío se realizó

correctamente”, cuando corresponda.

4. Versionado y cambios

•  Cualquier cambio en la estructura del evento debe ser versionado (ej. v1, v2) y

comunicado con anticipación.

•  Cambios que rompan compatibilidad (breaking changes) requieren un período de

transición acordado entre ambos equipos.

5. Dueños del contrato
Rol

Equipo

Contacto

Dueño del contrato

Panel Organizador

[nombre/usuario]

Consumidor principal

Notificaciones

Gabriela Herrera

6. Pendientes a acordar (OPCIONAL PREVIO ACUERDO)
•  ☐ Confirmar protocolo (REST vs evento asíncrono vs gRPC).
•  ☐ Confirmar nombre exacto del endpoint y autenticación.
•  ☐ Confirmar SLA de tiempo de respuesta.
•  ☐ Confirmar manejo de reintentos/errores.

