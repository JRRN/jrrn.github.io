---
layout: post
title: Leader Election
tags: Arquitectura
---

Hola a todos, volvemos esta vez con Leader Election.

Antes de entrar en detalle os explicaré un poquito de teoría sobre la sincronización en sistemas distribuidos, que os sugiero, que ampliéis...

En sistemas distribuidos la coordinación de operaciones se realiza mediante algoritmos que se crearon hacen ya unas décadas, cómo [Lamport](https://es.wikipedia.org/wiki/Tiempos_lógicos_de_Lamport "Algoritmo de Lamport"), [Cristian](https://es.wikipedia.org/wiki/Algoritmo_de_Cristian "Algoritmo de Cristian"), [Berkeley](https://es.wikipedia.org/wiki/Algoritmo_de_Berkeley "Algoritmo de Berkeley"), etc...

Sin embargo, los que nos interesan son los algoritmos de Exclusión Mutua:

- [Algoritmo_centralizado](https://es.wikipedia.org/wiki/Exclusión_mutua_en_sistemas_distribuidos#Algoritmo_centralizado "Algoritmo centralizado") 
- [Anillo Token-Ring](https://es.wikipedia.org/wiki/Exclusión_mutua_en_sistemas_distribuidos#Algoritmo_en_anillo_(Token_Ring) "Algoritmo en anillo")
- [Algoritmo de cola de prioridad compartida](https://es.wikipedia.org/wiki/Exclusión_mutua_en_sistemas_distribuidos#Algoritmo_de_cola_de_prioridad_compartida "Algoritmo de cola de prioridad compartida")
- [Algoritmo de Ricart y Agrawala](https://es.wikipedia.org/wiki/Exclusión_mutua_en_sistemas_distribuidos#Algoritmo_de_Ricart_y_Agrawala "Algoritmo de Ricart y Agrawala")
- [Algoritmo de Maekawa](https://es.wikipedia.org/wiki/Exclusión_mutua_en_sistemas_distribuidos#Algoritmo_de_Maekawa "Algoritmo de Maekawa")

Todos estos algoritmos se usan para que, teniendo varias máquinas, la coordinación entre los procesos se realice de la mejor forma, ordenada y lo más optimizada posible.

Con esto llegaríamos al ejemplo, que nos introducirá en el patrón.

Imaginemos que tenemos un servicio que por detrás ejecuta varios procesos, (agregar fondos, calcular saldo, guardar balance final y retirar fondos). Hoy en día con la fragmentación de los monolíticos tenemos operaciones independientes que ejecutan su parte, aislados de saber el estado y resultado del resto de operaciones. Sumado a la escalabilidad, implica que podemos tener ese servicio replicado con lo que las peticiones ya no se limitan a un solo punto de entrada, sino que pueden ser paralelas, asíncronas y en el mismo momento. Empezáis a ver el problema, ¿no?

Bien, pues con Leader Election, lo que hacemos es elegir una instancia como maestra, para que todas esas peticiones que se realicen y la ejecución de esos procesos que se realizan por detrás, acaben volviendo a la instancia maestra para acabar de marcar la petición como finalizada y procesarla.

Es como una transacción de bases de datos distribuida en la que se ejecutan las consultas por separado y hay un proceso esperando recibir los estados de finalizado de todas ellas, tomar el control y realizar el commit para persistir los cambios.

Para ello, no nos queda otra cosa que decidirnos por el algoritmo que mejor se ajuste a nuestras necesidades y aplicar el patrón Leader Election en nuestra infraestructura.

Os dejo un link con un repositorio de ejemplo: [Leader Election](https://github.com/mspnp/cloud-design-patterns/tree/master/leader-election "Source Example Leader Election"), en el que x procesos intentan acceder a un blob storage para pelearse por el recurso.

Un saludo y hasta pronto.
