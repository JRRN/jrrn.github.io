---
layout: post
title: Patrones de diseño Cloud
tags: Arquitectura
---

Hola de nuevo. Volviendo al tema de las arquitecturas, esta vez revisaremos los patrones de diseño orientados al Cloud. A diferencia de los patrones de diseño, un mismo patrón nos puede ofrecer varias soluciones para los principales problemas comunes en nuestras arquitectura cloud.

Para ello, dividiremos los patrones cloud según el enfoque al que están orientados. Pasamos a enumerarlos:

### Patrones de Disponibilidad ###

- [Monitor de salud](health-endpoint-monitoring "Monitor de salud")
- Queue-Based Load Leveling
- Throttling

### Patrones de Administración de datos ###

- Cache-Aside
- CQRS
- Event Sourcing
- Index Table
- Materialized View
- Sharding
- Static Content Hosting
- Valet Key

### Patrones de Diseño e implementación ###

- Ambassador
- Anti-Corruption Layer
- Backends for Frontends
- CQRS
- Compute Resource Consolidation
- External Configuration Store
- Gateway Aggregation
- Gateway Offloading
- Gateway Routing
- Leader Election
- Pipes and Filters
- Sidecar
- Static Content Hosting
- Strangler

### Patrones de Mensajería ###

- Comprobación de notificaciones
- Competing Consumers
- Pipes and Filters
- Priority Queue
- Publisher-Subscriber
- Queue-Based Load Leveling
- Scheduler Agent Supervisor

### Patrones de Administración y supervisión ###

- Ambassador
- Anti-Corruption Layer
- External Configuration Store
- Gateway Aggregation
- Gateway Offloading
- Gateway Routing
- Health Endpoint
- Sidecar
- Strangler

### Patrones de Rendimiento y escalabilidad ###

- Cache-Aside
- CQRS
- Event Sourcing
- Index Table
- Materialized View
- Priority Queue
- Queue-Based Load Leveling
- Sharding
- Static Content Hosting
- Throttling

### Patrones de Resistencia ###

- Bulkhead
- Circuit Breaker
- Compensating Transaction
- Health Endpoint Monitoring
- Leader Election
- Queue-Based Load Leveling
- Retry
- Scheduler Agent Supervisor

### Patrones de Seguridad ###

- Federated Identity
- Gatekeeper
- Valet Key

Nos vemos en breve y empezamos.

Saludos.