---
layout: post
title: Materialized View
tags: Arquitectura
---

El patrón materialized view, nos sirve para tener datos fragmentados en diferentes tablas en una vista des normalizada. De esta forma, podemos consultar estos datos y recuperarlos de una manera óptima.

Vayamos al ejemplo para tener clara la situación y como este patrón nos ayuda a solucionarlo.

Imaginemos que nuestra aplicación tiene la siguiente estructura:

TABLA USUARIOS

|(*) id_user|userName|userLastName|
|:-:|:-:|:-:|
|1|Pitufo|Gruñón|
|2|Papá|Pitufo|
|3|Pitufo|Amoroso|
|4|Pitufo|Inteligente|
|5|Pitufo|Burlón|

TABLA USUARIO CABELLERA

|(*) id_cabellera|id_user|color|
|:-:|:-:|:-:|
|1|1|castaño|
|2|2|moreno|
|3|3|castaño|
|4|4|moreno|
|5|5|castaño|

Si quisiéramos obtener el color de pelo de los usuarios deberíamos hacer una join entre usuarios y cabellera. Imaginemos que, esta consulta fuera muy costosa. La solución pasa por tener una vista materializada pre calculada, como si fuera una caché, con este resultado almacenado y simplemente ejecutar nuestra consulta sobre esta vista:

VISTA USUARIO-CABELLERA

|(*) id_user|userName|userLastName| id_cabellera|color|
|:-:|:-:|:-:|:-:|:-:|
|1|Pitufo|Gruñón|1|castaño|
|2|Papá|Pitufo|2|moreno|
|3|Pitufo|Amoroso|3|castaño|
|4|Pitufo|Inteligente|4|moreno|
|5|Pitufo|Burlón|5|castaño|

Esta solución, nos brinda la capacidad de realizar esta acción de mejora en datos que no se actualizan con frecuencia. Si, por el contrario, estos datos cambian constantemente, esto nos obligaría a recalcular o regenerar las vistas y podría penalizarnos en vez de ayudarnos.

Sin más, hasta la próxima.


