---
layout: post
title: Queue-Based Load Leveling
tags: Arquitectura
---

El patrón Queue-Based Load Leveling, es un patrón que se utiliza para controlar y enumerar la carga masiva sobre un servicio.

Imaginemos que tenemos una api, esta api tiene una llamada que nuestra aplicación usa de forma masiva cuando los usuarios usan nuestra aplicación. Imaginemos, también, que esa petición recibe cada día a las 9 de la mañana la solicitud de "dame las noticias para hoy", y aún más, imaginemos que nos lo solicitan los terrícolas y los [Klingons](https://es.wikipedia.org/wiki/Klingon "Klingons"), porque quieren saber como va el IBEX35... Con este nivel de peticiones, nuestro servicio por muy escalado que estuviera, recibiría un impacto de solicitudes que tardaría en procesar (penalizaríamos en rendimiento) o nos tumbaría en disponibilidad.

![NoQueue-BasedLoadLeveling](/img/cloudpatterns/NoQueue-BasedLoadLeveling.png "NoQueue-BasedLoadLeveling")

 Con Queue-Based Load Leveling lo que hacemos es refactorizar lo que sería una llamada clásica sobre un método de la api, donde el controlador llamaría al servicio y éste ejecutaría el código de acceso a los datos, en un mensaje sobre una cola, donde el servicio procesaría, por orden de entrada, los mensajes que van entrando.

De esta forma, a pesar de que el servicio tiene que responder muchas peticiones, nuestro rendimiento y nuestra disponibilidad no se vería tan afectada.

![Queue-BasedLoadLeveling](/img/cloudpatterns/Queue-BasedLoadLeveling.png "Queue-BasedLoadLeveling")

Pero... No todo el monte es orégano.

Sabemos que este patrón nos ayuda con la sobrecarga y la disponibilidad de la infraestructura, pero no siempre podremos implementar este patrón, ya que para usarlo deberemos implementar y adaptar nuestro código a obtener respuestas con una latencia superior. Sí, que tardaremos más en responder las solicitudes, con lo que no podremos tener peticiones y respuestas de una forma síncrona como suele ocurrir en una api. Pero tranquilos, que esta tecnología existe, tenemos por ejemplo [SignalR](https://docs.microsoft.com/es-es/aspnet/signalr/overview/getting-started/introduction-to-signalr "SignalR") entre otras.

Un saludo y hasta la próxima.
