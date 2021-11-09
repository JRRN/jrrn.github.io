---
layout: post
title: Priority Queue
tags: Arquitectura
---

Priority queue, es un patrón que nos ayuda a procesar las solicitudes en un orden específico. Tal y cómo dice su nombre es tratar cada petición según un criterio, llámese criterio a un flag de prioridad, que especifiquemos en nuestra lógica de peticiones y mensajería. ¿Y porque de este patrón?

Como sabemos, los mensajes dentro de un sistema orientado a colas o topis/subscriptores, (hago un inciso y simplifico la diferencia, colas 1 a 1, 1 mensaje, 1 consumidor, topic/subscriptores, 1 a N, 1 mensaje, varios consumidores), se procesan en orden FIFO, el primero en llegar, es el primero es salir, sin embargo, con este patrón podremos aplicar otros algoritmos como LIFO (last in, first out) o FEFO (first expired, first out) según el flag que hayamos definido para este propósito.

Vamos con el ejemplo. Imaginemos que nos dedicamos a la venta a por mayor. Hemos creado una aplicación que recoge los pedidos de nuestros clientes. Así, como tenemos un volumen de negocio bastante alto y procesamos nuestros pedidos con una arquitectura orientada a mensajes podemos estar en la mitad del océano y en el yate que nos proporciona este volumen alto de ventas. 

Como sabemos no es lo mismo gestionar 10 lápices que 2 millones de lápices. Así en nuestro sistema podemos tener varias reglas que según la cantidad del pedido acelere su gestión para poder coordinar todo ese gran volumen de lápices y que eso no nos impida seguir nadando entre tiburones.

Tan simple como esto, si nuestra api detecta un rango de cantidades dentro de las reglas de negocio definidas para gestionar la prioridad del pedido. Marcaremos con un flag de procesamiento más o menos alto para cumplir con los tiempos de nuestros clientes.

Por otro lado, hay sistemas de mensajería en los que puedes definir reglas y a partir de estas el mensaje es clasificado. Azure Service Bus es uno de ellos.

Sin embargo, si nuestro sistema de mensajería no admite reglas en los mensajes, la alternativa que nos queda es aplicar estas reglas en código y que sea este el que clasifique en un sistemas de colas/topics los mensajes según su prioridad.

 
![Priority Queue](/img/cloudpatterns/priority-queue.png "Priority Queue")


Un saludo y hasta la próxima.

