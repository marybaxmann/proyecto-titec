<!-- Slide number: 1 -->

TicketU
Venta de entradas para eventos universitarios, pagados y gratuitos
Proyecto de arquitectura de microservicios  ·  9 equipos + equipo de plataforma

Arquitectura de Software

### Notes:

<!-- Slide number: 2 -->
De un monolito a microservicios
Mismo problema, dos formas de resolverlo — ahora lo construimos en equipo

Monolito
Microservicios
Una sola aplicación con todos los módulos
Una única base de datos compartida
Simple de levantar al inicio
Un cambio pequeño obliga a redesplegar todo
Difícil de repartir en 9 equipos sin pisarse
Un servicio por equipo, con su propia base de datos
Comunicación vía API Gateway y broker de eventos
Cada equipo despliega y escala su parte por separado
Requiere coordinar contratos entre servicios
Así se organiza este proyecto
TicketU · Proyecto de arquitectura de microservicios
2

### Notes:

<!-- Slide number: 3 -->
El dominio: TicketU
Venta y gestión de entradas para eventos de la universidad
Fiestas de generación, campeonatos deportivos, charlas y seminarios. Algunos eventos se cobran, otros son gratuitos — y la plataforma debe manejar ambos casos con el mismo flujo de emisión de entradas.

Evento gratuito
Ej: charla, seminario, panel de egresados
Reserva → entrada con QR, sin pasar por pago
Catálogo de eventos, pagados y gratuitos

Compra o reserva de entradas

Evento pagado
Pago solo cuando el evento lo requiere

Ej: fiesta de generación, campeonato deportivo
Compra → checkout de pago → entrada con QR
Validación de entradas por QR en la puerta

Notificaciones y reseñas post-evento

TicketU · Proyecto de arquitectura de microservicios
3

### Notes:

<!-- Slide number: 4 -->
Arquitectura general
API Gateway al frente, un microservicio por equipo, broker de eventos entre ellos

App web / móvil

API Gateway

Auth

Catálogo

Entradas

Pagos

Check-in

Reseñas

Panel org.

Notif.

Promos

Broker de eventos
Cada recuadro es un microservicio con su propia base de datos; Entradas y Pagos se coordinan de forma asíncrona por el broker.
TicketU · Proyecto de arquitectura de microservicios
4

### Notes:

<!-- Slide number: 5 -->
9 equipos, 9 microservicios
Cada equipo es dueño de su backend y de su parte del frontend

Auth
Catálogo de eventos
Entradas / inventario

1

2

3
Login y registro
Listado y detalle de eventos
Emisión y stock de tickets

Pagos
Check-in
Reseñas

4

5

6
Checkout para eventos pagados
Validación de entradas por QR
Calificación de eventos

Panel organizador
Notificaciones
Promociones

7

8

9
Gestión de eventos
Avisos y recordatorios
Códigos de descuento
TicketU · Proyecto de arquitectura de microservicios
5

### Notes:

<!-- Slide number: 6 -->
Responsabilidad de backend y frontend
Cada equipo entrega su microservicio y la parte de interfaz que lo consume
| Equipo | Servicio | Backend | Frontend |
| --- | --- | --- | --- |
| 1 | Auth | Login, registro, sesión | Pantallas de login y registro |
| 2 | Catálogo de eventos | Eventos, tipo (gratis/pago) y precio | Home y detalle de evento |
| 3 | Entradas / inventario | Stock y emisión de entrada + QR | Selección de entradas y confirmación |
| 4 | Pagos | Cobro y confirmación de pago | Checkout de pago |
| 5 | Check-in | Validación de entradas por QR | App de validación en la puerta |
| 6 | Reseñas | Calificación de eventos pasados | Pantalla de reseñas |
| 7 | Panel organizador | Creación y gestión de eventos | Dashboard del organizador |
| 8 | Notificaciones | Avisos de compra y recordatorios | Centro de notificaciones |
| 9 | Promociones | Códigos y descuentos (solo pagados) | Aplicar código en checkout |
TicketU · Proyecto de arquitectura de microservicios
6

### Notes:

<!-- Slide number: 7 -->
Flujo especial: evento gratuito vs. pagado
Entradas y Pagos se coordinan por evento, no con una llamada directa

Selecciona evento

¿Evento gratuito?

Sí
No

Evento gratuito — sin pago
Checkout de pago
Equipo 3
Equipo 4

Emitir entrada + código QR
Equipo 3

Validación en la puerta — lectura de QR
Equipo 5
TicketU · Proyecto de arquitectura de microservicios
7

### Notes:

<!-- Slide number: 8 -->
Equipo plataforma (ayudante)
Responsabilidades transversales que no tienen dueño natural entre los 9 equipos

API Gateway
Broker de eventos
CI/CD y Docker
Única puerta de entrada hacia los 9 microservicios
Infraestructura de mensajería asíncrona entre servicios
Pipeline base y plantillas de contenedor para cada equipo

Frontend shell
Design system
Observabilidad
Layout y navegación donde cada equipo monta su fragmento
Componentes visuales compartidos para una UI coherente
Logging y monitoreo centralizado de los 9 servicios
TicketU · Proyecto de arquitectura de microservicios
8

### Notes:

<!-- Slide number: 9 -->
Stack y despliegue
Mismo criterio para los 9 equipos, para que todo se integre sin fricción

1

2

3

4
Backend
Datos
Contenedores
Despliegue
Node.js por servicio, expuesto vía REST detrás del Gateway
MongoDB — una base de datos propia por microservicio
Docker; cada equipo entrega su propio Dockerfile
On-premise, en la sala de servidores del curso

Regla de integración
Cada servicio publica su contrato de API (OpenAPI) antes de integrarse. Los eventos entre servicios — como el aviso de pago aprobado — se coordinan por el broker, nunca con una llamada directa entre dos equipos.
TicketU · Proyecto de arquitectura de microservicios
9

### Notes:

<!-- Slide number: 10 -->

¿Preguntas?
Formen sus 9 equipos y elijan qué microservicio quieren desarrollar.
TicketU — Proyecto de arquitectura de microservicios

### Notes: