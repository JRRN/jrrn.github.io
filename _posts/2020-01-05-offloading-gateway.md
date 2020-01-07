---
layout: post
title: Offloading Gateway
tags: Arquitectura
---

Hola de nuevo. Pues hoy toca el patrón Offloading Gateway. Este patrón es un patrón de optimización para nuestros servicios internos. Lo que nos dice este patrón es que simplifiquemos y unifiquemos los servicios genéricos que tenemos en nuestros servicios y los centralicemos en un punto único para reducir complejidad y fallos.

Si lo digo siempre, "S" single responsability y KISS deberían estar a fuego en nuestras cabezas.

Vamos con el ejemplo y así se entenderá mejor.

Imaginemos que tenemos varias APIS, en las que como es lógico y normal, y tenemos una validación de usuarios mediante un bearer token. En cada una de nuestra APIS realizamos el mismo proceso, llega una llamada, deserializamos el token, lo validamos contra el OAuth y dejamos pasar en función de la respuesta de nuestro servicio de autorización.

![Bad Offloading Gateway](/img/cloudpatterns/bad_offloading_gateway.png "Bad Offloading Gateway")

Esta lógica esta repetida en las tres APIS, y si en algún desarrollo se nos va el dedo, puede ser que tengamos 2 de las 3 APIS funcionando correctamente, y estemos dando palos de ciego buscando que hay mal en el código, cuando el error es que alguno actualizó los paquetes Nuget del Identity Server y ni se dio cuenta.

Pues bien, como dice el Offloading Gateway, para que esto no ocurra, tengamos más controlado el servicio de autorización y no tengamos el mismo código repetido tres veces. Propondríamos la siguiente infraestructura:

![Offloading Gateway](/img/cloudpatterns/good_offloading_gateway.png "Offloading Gateway")

Donde las tres APIS que antes consumíamos directamente ya no quedarían expuestas al usuario, si no que el usuario tendría la visibilidad del Offloading Gateway, que sería el encargado de realizar la autorización.

Del Offloading Gateway a las tres APIS, pasaríamos los parámetros necesarios en las llamadas con las propiedades que hayamos deserializado en el Offloanding Gateway y aplicaríamos una seguridad de [Valet Key](valet-key "Valet Key") en esta comunicación, un apikey o simplemente si no es necesario, podríamos estas APIS de forma no pública (no visibles desde el exterior) en nuestra red de Azure y ya, por ejemplo.

Un saludo.
