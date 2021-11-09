---
layout: post
title: Publisher-Subscriber
tags: Arquitectura
---

Hola de nuevo, después de mucho tiempo...

Hoy toca ver publisher-subscriber. Este patrón lo que nos permite es ejecutar de forma asíncrona operaciones después de que otro proceso notifique la ejecución con un evento. Es decir, es una arquitectura basada en eventos donde podemos tener un emisor y uno o varios consumidores, donde el emisor desencadena la comunicación a través de un mensaje y se desentiende de los perceptores de ese mensaje. Una vez, el/los receptor/es es notificado/s de que tienen un mensaje de entrada, desencadena/n su propia ejecución.

La principal diferencia entre los consumidores es saber la relación de mensajes 1 a 1 o 1 a varios. Según nuestra necesidad el modelo se enfoca hacia colas (1a1) o tópicos (1aN).

Es un modelo enfocado en aplicaciones distribuidas, (muerte al monolito) :skull:.

El principal beneficio que nos aporta este patrón es poder absorber más capacidad de peticiones sin tener que tener grandes máquinas para su procesamiento y el hecho de que el emisor de la petición no tiene que esperar una respuesta.

Su principal desventaja es que es un modelo asíncrono y que las respuestas se postergan en el tiempo según la cola de procesamiento.

Es decir, si vas a la papelería y le dices al dependiente "me das un lápiz", él va a buscarlo y te vas a tu casa con un lápiz en ese momento. Sin embargo, buscando el símil con esta arquitectura, si le dices a una tienda online "dame un lápiz", el te dice que ok y entonces tienes que esperar a que llegue a tu casa el lápiz para tener lápiz. 

Síncrono, te vas a la tienda. Asíncrono lo compras por internet y cuando llegue lo tienes.


![Publisher-Subscriber](/img/cloudpatterns/publisher-subscriber.png "Publisher-Subscriber")

Un saludo y hasta la próxima.

