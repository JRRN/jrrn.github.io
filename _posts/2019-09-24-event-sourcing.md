---
layout: post
title: Event Sourcing
tags: Arquitectura
---

El patrón Event Sourcing nos ayuda con el diseño y la implementación de nuestra aplicación. Es un patrón que se basa en almacenar todos lo cambios realizados sobre una entidad de dominio.

Este patrón nos ayuda a saber porque estados a pasado una entidad y en caso de producirse un fallo irrecuperable, poder reprocesar los estados almacenados dejando la estructura de datos de nuevo con el último estado que tenía (mantener la coherencia de datos) o realizar modificaciones manuales para compensar algún error, a través de un evento.

Este patrón nos ayuda a mitigar los problemas de las arquitecturas CRUD con muchas peticiones concurrentes.

Imaginemos que tenemos 2 usuarios (A, B) que van a interactuar con una misma entidad, y que por cosas del espacio-tiempo las dos transacciones llegan al mismo tiempo a la base de datos para modificar esta entidad. Podría ser, que por mala fortuna, la petición B que debería procesarse posterior a la de A, modifique la entidad y que seguidamente A la volviera a modificar. En este caso obtendríamos una inconsistencia de datos en esa entidad, con lo que la veracidad de la información quedaría anulada.

Con event sourcing, podemos solventar este problema, ya que los eventos de A y B tienen una marca de tiempo, con lo que nos permite procesar estos eventos cronológicamente como sucede con los [Relojes de Lamport](https://es.wikipedia.org/wiki/Tiempos_lógicos_de_Lamport "Relojes de Lamport").

Los principales beneficios de Event Sourcing son:

- Almacenamos todos los eventos que hacen mutar una entidad.

- Como la emisión y el procesamiento de los eventos van por separado, nos permite mejor rendimiento y escalabilidad.

- Tenemos una trazabilidad para verificar, modificar o eliminar cambios en una entidad y sabemos quien y cuando se ha desencadenado este evento.

- Mejoramos la consistencias de datos ya que no se producen modificaciones simultaneas sin controlar el orden en nuestra base de datos.

- Casa muy bien con el patrón CQRS.

Veamos la representación de esta arquitectura en el Cloud:

![Event Sourcing](/img/cloudpatterns/eventsourcing.png "Event Sourcing")

Un saludo.
