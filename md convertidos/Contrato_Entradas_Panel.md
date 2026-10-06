Contrato de interfaz: Entradas / Inventario ↔ Panel Organizador

Versión: 1.0

Equipo consumidor: Entradas / Inventario

Equipo proveedor: Panel Organizador

Basado en: Matriz de Dependencia de Datos y necesidad de validación/sincronización (Pull).

# 1. Propósito

El equipo de Entradas/Inventario (consumidor) necesita consultar al microservicio de Panel Organizador (proveedor) los datos maestros de un evento específico. Aunque normalmente el Panel "empuja" (Push) la creación del evento hacia Entradas, esta operación de "Pull" (Consulta) es vital para que Entradas pueda solicitar y validar los detalles actualizados del evento (como fecha, hora, tipo de entrada y aforo límite) en caso de pérdida de sincronización, auditoría o recuperación ante caídas del sistema.

# 2. Operación: Consultar Detalles de Evento (obtener\_detalles\_evento)

## 2.1 Descripción

Permite al servicio de Entradas consultar la fuente de verdad del organizador para obtener la configuración base e inmutable de un evento.

## 2.2 Quién la expone

Equipo Panel Organizador.

## 2.3 Quién la consume

Equipo Entradas / Inventario, en el momento en que necesite validar si un evento sigue vigente, si sus características (pago/gratis) han cambiado o para rehidratar su base de datos local.

## 2.4 Endpoint propuesto

GET /api/v1/panel/eventos/{id\_evento}

## 2.5 Request (lo que se envía)

|  |  |  |  |
| --- | --- | --- | --- |
| Campo | Tipo | Obligatorio | Descripción |
| id\_evento (En URL) | string | Sí | Identificador único del evento que se desea consultar. |

Ejemplo Request:

GET /api/v1/panel/eventos/evt-77889

## 2.6 Response (lo que se recibe)

|  |  |  |  |
| --- | --- | --- | --- |
| Campo | Tipo | Obligatorio | Descripción |
| id\_usuario | string | Sí | ID del usuario organizador dueño del evento. |
| nombre\_evento | string | Sí | Nombre público del evento. |
| fecha\_evento | string | Sí | Fecha en la que se realizará el evento. |
| hora\_evento | string | Sí | Hora de inicio del evento. |
| cantidad\_entradas | integer | Sí | Aforo máximo permitido para el evento. |
| tipo\_entrada | string | Sí | Categoría de la entrada (pago o gratis). |
| estado\_evento | string | Sí | Estado actual en el panel (ej. ACTIVO, CANCELADO). |

Ejemplo:

{
 "id\_usuario": "org-4455",
 "nombre\_evento": "Fiesta Mechona Info",
 "fecha\_evento": "2026-11-20",
 "hora\_evento": "22:00",
 "cantidad\_entradas": 500,
 "tipo\_entrada": "pago",
 "estado\_evento": "ACTIVO"
}

Nota de diseño: El Panel provee únicamente los datos duros operativos que impactan la emisión de tickets. Descripciones largas o imágenes se omiten para optimizar la carga.

## 2.7 Códigos de error

|  |  |
| --- | --- |
| Código | Significado |
| 400 | Formato de id\_evento inválido. |
| 404 | Evento no encontrado en los registros del Panel. |
| 500 | Error interno del servicio Panel Organizador. |

## 2.8 Tiempo de respuesta esperado (SLA)

< 300 ms (Operación de lectura simple).

# 3. Reglas de uso (lado consumidor)

1. Entradas debe utilizar este endpoint como mecanismo de validación o "fallback". Es decir, si el evento no existe en su base local o si hay discrepancias de aforo, consulta al Panel.
2. Al recibir un 404, Entradas debe asumir que el evento fue eliminado o no fue correctamente creado e invalidar temporalmente la venta para dicho evento.
3. Los datos obtenidos por Entradas (como fecha y hora) deben actualizarse en la base de datos local de Inventario si difieren.

# 4. Versionado y cambios

Si Panel Organizador agrega nuevos tipos de eventos o añade campos críticos (como restricciones de edad), debe lanzar una versión v2 del endpoint y notificar a Entradas.

# 5. Dueños del contrato

|  |  |  |
| --- | --- | --- |
| Rol | Equipo | Contacto |
| Dueño del contrato | Panel Organizador | [Representante de Panel] |
| Consumidor principal | Entradas / Inventario | Sebastián Fuentes (Scrum Master) |

# 6. Pendientes a acordar (OPCIONAL PREVIO ACUERDO)

☐ Confirmar con Panel Organizador si la comunicación de "Evento Creado" seguirá siendo un "Push" (POST de Panel a Entradas) y si este "Pull" (GET de Entradas a Panel) quedará solo como respaldo o validación.