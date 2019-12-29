---
layout: post
title: Patrones de diseño Cloud
tags: Arquitectura
---

Hola de nuevo. Volviendo al tema de las arquitecturas, esta vez revisaremos los patrones de diseño orientados al Cloud. A diferencia de los patrones de diseño, un mismo patrón nos puede ofrecer varias soluciones para los principales problemas comunes en nuestras arquitectura cloud.

Para ello, dividiremos los patrones cloud según el enfoque al que están orientados. Pasamos a enumerarlos:

### Patrones de Disponibilidad ###

- [Health EndPoint Monitoring](health-endpoint-monitoring "Health EndPoint Monitoring")
- [Queue-Based Load Leveling](queue-based-load-leveling "Queue-Based Load Leveling")
- [Throttling](throttling "Throttling")

### Patrones de Administración de datos ###

- [Cache Aside](cahe-aside "Cache Aside")
- [CQRS](cqrs "CQRS")
- [Event Sourcing](event-sourcing "Event Sourcing")
- [Index Table](index-table "Index Table")
- [Materialized View](materialized-view "Materialized View")
- [Sharding](sharding "Sharding")
- [Static Content Hosting](static-content-hosting "Static Content Hosting")
- [Valet Key](valet-key "Valet Key")

### Patrones de Diseño e implementación ###

- [Ambassador](ambassador "Ambassador")
- [Anti-Corruption Layer](anti-corruption-layer "Anti-Corruption Layer]")
- Backends for Frontends
- [CQRS](cqrs "CQRS")
- Compute Resource Consolidation
- External Configuration Store
- Gateway Aggregation
- Gateway Offloading
- Gateway Routing
- Leader Election
- Pipes and Filters
- Sidecar
- [Static Content Hosting](static-content-hosting "Static Content Hosting")
- Strangler

### Patrones de Mensajería ###

- Comprobación de notificaciones
- Competing Consumers
- Pipes and Filters
- Priority Queue
- Publisher-Subscriber
- [Queue-Based Load Leveling](queue-based-load-leveling "Queue-Based Load Leveling")
- Scheduler Agent Supervisor

### Patrones de Administración y supervisión ###

- [Ambassador](ambassador "Ambassador")
- [Anti-Corruption Layer](anti-corruption-layer "Anti-Corruption Layer]")
- External Configuration Store
- Gateway Aggregation
- Gateway Offloading
- Gateway Routing
- [Health EndPoint Monitoring](health-endpoint-monitoring "Health EndPoint Monitoring")
- Sidecar
- Strangler

### Patrones de Rendimiento y escalabilidad ###

- [Cache Aside](cahe-aside "Cache Aside")
- [CQRS](cqrs "CQRS")
- [Event Sourcing](event-sourcing "Event Sourcing")
- [Index Table](index-table "Index Table")
- [Materialized View](materialized-view "Materialized View")
- Priority Queue
- [Queue-Based Load Leveling](queue-based-load-leveling "Queue-Based Load Leveling")
- [Sharding](sharding "Sharding")
- [Static Content Hosting](static-content-hosting "Static Content Hosting")
- [Throttling](throttling "Throttling")

### Patrones de Resistencia ###

- Bulkhead
- Circuit Breaker
- Compensating Transaction
- [Health EndPoint Monitoring](health-endpoint-monitoring "Health EndPoint Monitoring")
- Leader Election
- [Queue-Based Load Leveling](queue-based-load-leveling "Queue-Based Load Leveling")
- Retry
- Scheduler Agent Supervisor

### Patrones de Seguridad ###

- Federated Identity
- Gatekeeper
- [Valet Key](valet-key "Valet Key")

Nos vemos en breve y empezamos.

Saludos.
