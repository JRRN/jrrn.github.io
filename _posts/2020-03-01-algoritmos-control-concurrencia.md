---
layout: post
title: Algoritmos de Control de Concurrencia en Sistemas Distribuidos 
tags: Arquitectura
---

Hola a todos, hoy os vengo a explicar los algoritmos de concurrencia en los sistemas distribuidos. Atentos por que viene chapa, aunque a mí, me parece la mar de interesante.

Empezamos con la forma en que los procesos se ejecutan en sistemas distribuidos y como se determina el orden, aunque hay más algoritmos ([Berkeley](https://es.wikipedia.org/wiki/Algoritmo_de_Berkeley "Berkeley") , [Marzullo](https://es.wikipedia.org/wiki/Algoritmo_de_Marzullo "Marzullo"), [Paxos](https://es.wikipedia.org/wiki/Algoritmo_de_Paxos "Paxos")) nos centraremos en los algoritmos de tiempos lógicos:

**Algoritmos de Tiempos Lógicos**

![Caso 1](/img/sistdist/case1.png "Caso 1")

***Algoritmo de Tiempos Lógicos de Lamport***

![Lamport](/img/sistdist/case1lamport.png "Lamport")


***Algoritmo de Vector de Tiempos Lógicos***

![Vector](/img/sistdist/case1vector.png "Vector")

---

![Caso 2](/img/sistdist/case2.png "Caso 2")

***Algoritmo de Tiempos Lógicos de Lamport***

![Lamport](/img/sistdist/case2lamport.png "Lamport")


***Algoritmo de Vector de Tiempos Lógicos***

![Vector](/img/sistdist/case2vector.png "Vector")

>Con los relojes de Lamport, podemos ver que existe un problema con los tiempos de los eventos, ya que tienen un valor superior respecto al anterior evento y no se puede saber, a ciencia cierta, cuando se ha producido el evento, ni el orden en que se produjeron.
>
>Sin embargo, con los relojes vectoriales podemos apreciar que cada evento mantiene su tiempo exacto, en todos los vectores y se puede seguir una cronología y obtener el orden de cuando han sucedido los eventos.

**Algoritmos de exlusión mútua:**

Los algoritmos de exclusión mutua ayudan a los sistemas distribuidos a solventar la forma en la que se coordinan en la ejecución de sus procesos, solventando los fallos que se puedan producir en esta coordinación (Resiliencia).

***Algoritmo basado en servidor central:***
Este algoritmo se basa en tener un servidor en el que se encolan las peticiones y es éste el que decide, según una cola de peticiones, el proceso que entra en ejecución, dando paso y recibiendo una confirmación de que este proceso ya ha acabado. De esta forma, el servidor puede dar paso al siguiente proceso de la cola.

A nivel de escalabilidad añadir un nuevo proceso o nodo, nos tiene grandes afectaciones, ya que el nuevo proceso o nodo, enviará su solicitud y entrará en la cola.

![Servidor Central](/img/sistdist/servidorcentral.png "Servidor Central")

***Algoritmo basado en un anillo:***
Este algoritmo propone que cada proceso esté conectado con otro proceso coordinando los mensajes (testigo) en una única dirección, lo que provoca tener que esperar a recibir el testigo para poder entrar en ejecución o pasar el testigo al siguiente proceso si no se tiene que entrar en ejecución.

A nivel de escalabilidad el simple hecho de escalar verticalmente, que es la adición o disminución de nodos, afecta al tiempo en recibir el testigo, en 'tiempo-nodos' añadidos o en 'tiempo-nodos' disminuidos y hay que actualizar la definición del nuevo anillo.

![Anillo](/img/sistdist/anillo.png "Anillo")

***Algoritmo de multidifusión y relojes lógicos:***
Este algoritmo propone que cada vez que un proceso necesita ejecutarse, este, envía una petición al resto de nodos y hasta que no recibe una respuesta afirmativa de todos o de N nodos, en el peor de los casos, este no entra en ejecución. Las peticiones se miden por tiempo.

A nivel de escalabilidad, añadir un nuevo nodo, implica que este último no entrará en ejecución hasta no haber completado todas las peticiones con tiempos anteriores y se deberá actualizar el computo de respuestas afirmativas.

![Lamport](/img/sistdist/lamport.png "Lamport")

***Algoritmo de votación de Maekawa:***
El algoritmo de Maekawa se basa en que todos los procesos que están involucrados son los responsables de dar el testigo para la ejecución al siguiente proceso siempre y cuando el estado de ejecución este libre.

Es decir, si la ejecución esta lista para ejecutar y los demás procesos dan el “visto bueno”, entonces se bloquea el estado de ejecución y se ejecuta. Una vez acabado, se libera el estado de ejecución y se realiza la votación para ver quien entra a ejecutarse, el que más votos tenga, es el que se ejecuta. 

A nivel de escalabilidad, en la siguiente votación, habrá un nodo o proceso más para votar y para solicitar el estado de ejecución, lo que implica que los demás nodos deben saber que hay uno nuevo para determinar nuevo número de respuestas a recibir para poder ejecutarse.

![Maekawa](/img/sistdist/maekawa.png "Maekawa")

Sin más, espero que os haya gustado y aclarado las dudas sobre estos algoritmos.

Un saludo.