---
layout: post
title: Caché Aside
tags: Arquitectura
---

El patrón Cache Aside nos permite devolver datos en una petición sin tener la necesidad de ir a la base de datos a buscarlos. Con este patrón reducimos el tiempo de acceso a los datos, reducimos el uso de recursos lo que hace que mejoremos el rendimiento de nuestra aplicación.

Una de las formas de aplicar este patrón la vimos en el artículo de como usar la [caché no distribuida](cache-no-distribuida "caché no distribuida") en NetCore.

Aunque lo recomendable para grandes infraestructuras en centralizar esta caché de forma distribuida.

Para ello, lo que propone este patrón lo representaremos en un diagrama:

![cache aside](/img/cloudpatterns/cache-aside.png "cache aside")

Como vemos tanto las peticiones realizadas por nuestra app o por nuestro site, se centralizan en nuestra api, esta emite una llamada sobre la caché redis, en la que si esta no contesta, baja a la base de datos a buscar los datos, los incorpora en la caché y los devuelve (marcadas las llamadas en azul), sin embargo, si la caché es capaz de procesar la solicitud, será esta quien responda (marcado como naranja) sin tener que acceder a la base de datos.

Sin embargo, antes de implementar este patrón se debe tener en cuenta:

- Determinar el tiempo validez de nuestros datos en la caché. Tenemos que pensar bien, que necesidad tenemos en que los datos sean lo más veraces, coherentes y consistentes posibles, aunque hay mecanismos de control en las cachés, puede ser que la respuesta que nos este dando no contenga los datos más actualizados que hay en la base de datos.

- Con el punto anterior se suma el tiempo de regeneración de la caché, esto quiere decir, cada cuanto tiempo la destruimos y la volvemos a regenerar. Para ello, debemos analizar que datos tiene mayor inmutabilidad y cuales menos.

- El tamaño de la caché, no debemos tener una caché que contenga la base de datos entera, esto no tiene sentido y no nos aportará ningún beneficio.

Un saludo.
