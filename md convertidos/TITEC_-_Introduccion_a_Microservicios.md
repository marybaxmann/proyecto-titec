<!-- Slide number: 1 -->
ARQUITECTURA DE SOFTWARE

MONOLITO
Introducción a
Microservicios

De la arquitectura monolítica a los sistemas distribuidos e independientes

API

Basado en “Microservices” de Martin Fowler (martinfowler.com) y en el lenguaje de patrones de microservices.io (Chris Richardson)

### Notes:

<!-- Slide number: 2 -->
AGENDA
Qué vamos a ver
01
El monolito: el punto de partida
05
Impacto en el trabajo en equipo

02
Qué es la arquitectura de microservicios
06
Organizaciones descentralizadas: modelo Spotify

03
Ejemplo comparado: FoodExpress
07
Desafíos técnicos de interoperabilidad

04
Para qué sirve: atributos de calidad
08
Proyecto práctico: esqueleto en GitHub
Introducción a Microservicios
2

### Notes:

<!-- Slide number: 3 -->
01 · PUNTO DE PARTIDA
El monolito: una aplicación, una unidad
Según Martin Fowler, una aplicación monolítica se construye como una única unidad ejecutable: la interfaz de usuario, la lógica de negocio y el acceso a datos viven en el mismo proceso.

Autenticación

Catálogo

Pedidos
VENTAJAS INICIALES
Simple de construir, ejecutar y probar en una sola máquina.
Un único pipeline de build y despliegue.
Buena opción para equipos y proyectos pequeños — no es un anti-patrón.

Pagos

Delivery

Notificaciones

Reseñas
FRICCIONES AL CRECER
Cualquier cambio, por pequeño que sea, exige reconstruir y redesplegar TODA la app.
Escalar significa escalar el proceso completo (vertical), aunque solo un módulo lo necesite.
Con el tiempo cuesta mantener límites modulares claros.
Todos comparten el mismo proceso y la misma base de datos
Introducción a Microservicios
3

### Notes:

<!-- Slide number: 4 -->
EJEMPLO · FOODEXPRESS
Monolito — vista de componentes

Aplicación Monolítica FoodExpress (Node.js)

Usuario

App Cliente

Auth

Catálogo

Pedidos

MongoDB
(única BD)

Pagos

Delivery

Notificaciones

Reseñas

Restaurante

Panel Restaurante

Todos los módulos comparten las mismas colecciones. Un cambio en “Pedidos” puede requerir volver a desplegar TODA la aplicación.
Introducción a Microservicios
4

### Notes:

<!-- Slide number: 5 -->
EJEMPLO · FOODEXPRESS
Monolito — vista de despliegue

Sala de servidores (on-premise)

Servidor único

Docker Host
HTTP :3000

Dispositivo
del usuario
HTTPS

Nginx
(Reverse Proxy)

Node.js — Aplicación Monolítica
(Auth + Catálogo + Pedidos +
Pagos + Delivery + Notif.)

MongoDB

TCP :27017

Escalar = comprar un servidor más grande. Si cae, cae TODA la aplicación.
Introducción a Microservicios
5

### Notes:

<!-- Slide number: 6 -->

![PlantUML diagram](Picture2.jpg)

![PlantUML diagram](Picture4.jpg)

### Notes:

<!-- Slide number: 7 -->
02 · DEFINICIÓN
Qué es la arquitectura de microservicios

Catálogo
Fowler y Lewis la definen como el desarrollo de una única aplicación como un conjunto de pequeños servicios, cada uno en su propio proceso, comunicándose mediante mecanismos livianos (a menudo HTTP), construidos alrededor de capacidades de negocio y desplegables de forma independiente.

Auth

Pedidos

microservices.io lo resume como una colección de servicios que son independientemente desplegables y débilmente acoplados, cada uno usualmente a cargo de un equipo pequeño.

Pagos

Cada servicio es un proceso independiente, con su propia base de datos
Gobierno y tecnología descentralizados: cada equipo elige su stack
Comunicación por “endpoints inteligentes, tuberías tontas” (HTTP / mensajería)
Automatización de infraestructura y despliegue continuo

Notif.

Delivery

Introducción a Microservicios
6

### Notes:

<!-- Slide number: 8 -->
EJEMPLO · FOODEXPRESS
Microservicios — vista de componentes

Usuario

App Cliente

Auth
Service

DB

Catalog
Service

DB

publica “pedido_creado”

Orders
Service

DB

Message
Broker
(RabbitMQ)

API
Gateway

Payments
Service

DB

eventos consumidos de forma asíncrona

Delivery
Service

Restaurante

Panel Rest.

DB

Los servicios NO se llaman directamente para eventos. Cada servicio tiene su propia BD (Database per Service).

Notification
Service

DB

Introducción a Microservicios
7

### Notes:

<!-- Slide number: 9 -->
EJEMPLO · FOODEXPRESS
Microservicios — vista de despliegue

Sala de servidores (on-premise) — 3 servidores independientes

Servidor 1
Servidor 2
Servidor 3

API Gateway

Orders Service

Delivery Service

Auth Service

Orders DB

Delivery DB

Dispositivo
del usuario

Balanceador
(Nginx)

Auth DB

Payments Service

Notification Svc

Catalog Service

Payments DB

RabbitMQ Broker

Catalog DB

Cada servicio despliega y escala de forma independiente. Si “Delivery” cae, el resto sigue funcionando.
Introducción a Microservicios
8

### Notes:

<!-- Slide number: 10 -->

![PlantUML diagram](Picture2.jpg)

### Notes:

<!-- Slide number: 11 -->

![PlantUML diagram](Picture4.jpg)

### Notes:

<!-- Slide number: 12 -->
SÍNTESIS
Monolito vs. microservicios, en una mirada

Monolito

Microservicios

Despliegue
Una unidad completa
Servicios independientes
Escalado
Vertical, todo junto
Horizontal, por servicio

Base de datos
Única y compartida
Una por servicio (polyglot)
Ante un fallo
Puede caer toda la app
Aislado al servicio afectado

Tecnología
Un solo stack
Distintos lenguajes/BD por equipo
Organización de equipos
Por capa técnica
Por capacidad de negocio
Introducción a Microservicios
9

### Notes:

<!-- Slide number: 13 -->
04 · PARA QUÉ SIRVE
Atributos de calidad que se potencian

1

2

3

4

5
Escalabilidad selectiva
Resiliencia
Desplegabilidad
Evolutividad
Diversidad tecnológica
Escala solo el servicio bajo demanda (ej. Pedidos en hora punta), no toda la aplicación.
El “diseño para el fallo” aísla los problemas: si un servicio cae, el resto sigue funcionando.
Cada servicio se libera de forma independiente y frecuente — entrega continua real.
Un servicio puede reescribirse o reemplazarse sin tocar el resto del sistema.
Persistencia políglota: cada equipo elige el lenguaje y la base de datos más adecuados.
Introducción a Microservicios
10

### Notes:

<!-- Slide number: 14 -->
05 · PERSONAS Y EQUIPOS
Cómo cambia el trabajo en equipo

→
Equipos independientes

⇄
...que igual deben sincronizarse
Los servicios se organizan alrededor de capacidades de negocio, no de capas técnicas — el equipo es multifuncional (UX, backend, datos) y dueño de su servicio de punta a punta.
Equipos pequeños tipo “two-pizza team”: pueden decidir y desplegar sin depender de aprobaciones cruzadas.
Mentalidad de producto, no de proyecto — “you build it, you run it”: el equipo opera lo que construye.
La autonomía no elimina la coordinación: los contratos de API son el punto de acuerdo entre equipos.
Patrones como “Tolerant Reader” y Consumer-Driven Contracts permiten evolucionar cada servicio sin romper a los demás.
El versionado se usa como último recurso; se prefiere diseñar servicios tolerantes a cambios.
Introducción a Microservicios
11

### Notes:

<!-- Slide number: 15 -->
06 · ORGANIZACIÓN DESCENTRALIZADA
Compatible con modelos descentralizados: el modelo Spotify
https://www.atlassian.com/es/agile/agile-at-scale/spotify
Los microservicios encajan de forma natural con estructuras organizacionales pensadas para la autonomía, como el modelo popularizado por Spotify (Kniberg & Ivarsson).

Squad
Tribe
Chapter
Guild
Equipo pequeño y multifuncional, dueño de una misión de punta a punta.
Conjunto de squads en un área de negocio relacionada.
Comunidad por disciplina que alinea estándares entre squads.
Comunidad de interés voluntaria, cruza tribus.

≈ 1 o más microservicios

≈ un dominio de negocio

≈ gobierno descentralizado con herramientas compartidas

≈ prácticas comunes entre equipos
La idea clave: la autonomía técnica de los microservicios (desplegables por separado) y la autonomía organizacional de los squads (deciden y entregan sin esperar a otros) se refuerzan mutuamente — el límite de servicio y el límite de equipo tienden a coincidir.
Introducción a Microservicios
12

### Notes:

<!-- Slide number: 16 -->
07 · DESAFÍOS TÉCNICOS
Interoperabilidad: coreografía vs. orquestación

COREOGRAFÍA
ORQUESTACIÓN

Payments

Orquestador
(Saga)

Orders

Notif.

Notif.

Payments

Delivery

Delivery
Cada servicio reacciona a eventos por su cuenta; no hay un controlador central.
Un componente central decide y coordina la secuencia de llamadas a los demás servicios.
Comunicación síncrona vs. asíncrona:
Fowler advierte que encadenar llamadas síncronas multiplica los tiempos de caída (“synchronous calls considered harmful”). Por eso el estilo de microservicios favorece “endpoints inteligentes, tuberías tontas”: mensajería asíncrona sobre un bus simple (RabbitMQ, Kafka) en vez de un ESB centralizado con lógica de orquestación embebida.
Introducción a Microservicios
13

### Notes:

<!-- Slide number: 17 -->
07 · DESAFÍOS TÉCNICOS
Eventos, colas y patrones de diseño

API Gateway
Saga
Circuit Breaker

Punto único de entrada que enruta y compone respuestas hacia los clientes.
Secuencia de transacciones locales con compensaciones, para mantener consistencia sin transacciones distribuidas.
Corta llamadas a un servicio que falla repetidamente, evitando fallos en cascada.

Domain Event / Broker
Service Discovery
CQRS / API Composition

Un servicio publica eventos de dominio; otros los consumen de forma asíncrona (RabbitMQ, Kafka).
Registro que permite a los servicios encontrarse entre sí en tiempo de ejecución.
Combina datos de varios servicios para responder consultas que cruzan sus límites.
Lenguaje de patrones completo: microservices.io/patterns
Introducción a Microservicios
14

### Notes:

<!-- Slide number: 18 -->

![](Imagen21.jpg)
08 · MANOS A LA OBRA
Proyecto práctico: esqueleto de microservicios
Un mini ecosistema de 3 servicios independientes para practicar composición y comunicación entre microservicios, cada uno con su propio Dockerfile, docker-compose y contrato OpenAPI.

REPOSITORIO EN GITHUB
FWizav / skeletotitec
github.com/FWizav/skeletotitec
sandwich-base-service

Incluye red Docker compartida, instrucciones de arranque por servicio y ejemplos con curl para probar el flujo completo.
Registra la base del sándwich
sandwich-mermelada-service

Agrega mermelada y consulta al servicio de base
Cada servicio se levanta por separado (docker compose up en cada carpeta) y se comunican entre sí vía HTTP — una base sencilla para luego incorporar broker de eventos, API Gateway y demás patrones vistos.
sandwich-tapa-service

Agrega la tapa y consulta a base + mermelada
Introducción a Microservicios
15

### Notes:

<!-- Slide number: 19 -->
CONCURSO!!!
Recursos y cierre
Para profundizar en lo visto hoy

El artículo de referencia sobre las características de la arquitectura de microservicios.
Martin Fowler — “Microservices”

martinfowler.com/articles/microservices.html

El lenguaje de patrones de Chris Richardson: colaboración entre servicios, despliegue, resiliencia y más.
microservices.io

microservices.io

Esqueleto de 3 microservicios para experimentar con lo aprendido.
Proyecto práctico — skeletotitec

github.com/FWizav/skeletotitec
¡Gracias! Preguntas y comentarios son bienvenidos.

### Notes: