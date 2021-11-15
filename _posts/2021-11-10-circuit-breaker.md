---
layout: post
title: Circuit Breaker
tags: Arquitectura
---

El patrón circuit breaker, es un patrón que no está enfocado a la infraestructura como quizá hemos podido ver en otros patrones. Y se desarrolla más en nuestro código. Sin embargo, este pedacito de código que desarrollamos otorga unos beneficios a la infraestructura tales cómo recuperación, robustez y resiliencia.

Circuit breaker es una analogía a los estados de los circuitos eléctricos. En estos, los estados son abierto o cerrado. Si el estado es abierto, no se produce movimiento de electrones y el circuito no funciona. Si el estado es cerrado, el paso de electrones se introduce en el circuito dándole funcionalidad.

Traduciendo esta analogía a nuestro código, la principal solución que nos aporta circuit breaker es poder abrir, semi-abrir o cerrar la conexión a los servicios.

Si nos situamos en una aplicación web, donde esta, está conectada a varios servicios, puede ocurrir que tengamos algún servicio con un error transitorio, pongamos que por lo que sea nuestro servicio se cae, error http 500. En ese momento, nuestra principal aplicación empezaría a levantar excepciones de conexión con el servicio y nuestro log se llenaría de excepciones. Los usuarios, intentan y reintentan el proceso. Y nuestra aplicación se empieza a volver inconsistente porque tiene que empezar a manejar más y más excepciones. Recordemos, que las excepciones cuestan dinero y en ciertos casos consumen sockets que no se pueden reutilizar. Si tuviéramos muchas peticiones, podríamos agotar los sockets de la máquina y entonces ahora sí, ya caería la web principal y afectaría a otros servicios que hasta ahora estaban funcionando con normalidad.

Menuda situación. Producción caído.

Bueno, pues aquí entra en juego Circuit Breaker. De la mano del patrón [Retry](patron-retry "Patrón Retry"), podemos detectar que el servicio está caído y relanzar N cantidad de reintentos con un lapso de tiempo prudencial y dilatando el tiempo de reintento en cada iteración, antes de decirle al usuario que el servicio no está disponible.

Simplificando. Configuramos que se produzcan 5 reintentos si la respuesta de un servicio es 500 y damos un retardo en cada reintento de (1 + it). 

Primera llamada, nos devuelve un 500, se abre el circuito, 1+(it=0)=1, me espero 1 segundo antes de relanzar siguiente iteración de petición. 
Segunda llamada, nos devuelve un 500, se mantiene el circuito abierto, 1+(it=1)=2, me espero 2 segundos antes de relanzar siguiente iteración de petición. 
Tercera llamada, nos devuelve un 500, se mantiene el circuito abierto, 1+(it=2)=3, me espero 3 segundos antes de relanzar siguiente iteración de petición. 
Cuarta llamada, nos devuelve un 500, se mantiene el circuito abierto, 1+(it=3)=4, me espero 4 segundos antes de relanzar siguiente iteración de petición. 
Quinta llamada, nos devuelve un 500, se mantiene el circuito abierto, 1+(it=5)=5, me espero 5 segundos antes de relanzar siguiente iteración de petición. 
No se produce sexta llamada y devolvemos al usuario que el servicio no está disponible.

Sin embargo, si en el transcurso de las iteraciones, el servicio se recupera, entonces se cierra el circuito y volvemos a la normalidad.

Para implementar esta parte del código [Polly](https://github.com/App-vNext/Polly "Polly") tiene extensiones para poder gestionarlo de una manera muy sencilla a través de policy.

Vale, pero no es todo tan bonito. Porque igual que podemos acabar con lo sockets si se producen muchas excepciones, podemos agotarlos si se producen muchos retries.

En definitiva, circuit braker nos ayuda con las intermitencias y las altas latencias en ciertos servicios, pero configurar circuit braker por defecto, considero, es una mala praxis.

Be water my friend! Un saludo.

