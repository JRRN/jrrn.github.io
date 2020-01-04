---
layout: post
title: Gateway Aggregation
tags: Arquitectura
---

¡Buenos días! Hoy vamos a hablar del patrón de implementación Gateway Aggregation. Tan querido por muchos y tan odiado por otros.

Para explicar este patrón vamos a necesitar un poco de contexto. Así que os muestros el problema:

![Gateway Aggregation](/img/cloudpatterns/gatewayaggregation.png "Gateway Aggregation")

> "¿Problema, Rafa? Pero si esto es canela fina. Vaya se ve claramente, tengo servicios independientes que hacen su llamada y dan su respuesta. Más 'S' Separación de Responsabilidades imposible, si lo único que te hace falta es cambiar esas APIS por un kubernetes y ya lo tienes 'to' hecho", os direís.

Pues bien, ¿y si os digo que es una buena idea lo que estaís haciendo y se llamada renderización por componentes?

Sin embargo, podemos darle una vuelta más de tuerca y optimizar ciertas llamadas.

Imaginemos que tenemos una web donde el usuario llega se loguea y llega a la home:

![Amazon Music](/img/cloudpatterns/amazonmusic.png "Amazon Music")

![Ikea](/img/cloudpatterns/ikea.png "Ikea")

Tenemos los casos de Ikea y Amazon Music.

Amazon Music realiza el patrón de agregación en su página home con un solo método GetHome, donde lo que hace es hacer una única petición y posteriormente en la parte de back, realiza todas la llamadas a los servicios internos, recopila la información, la "agrega" en un modelo, HomeModel y la devuelve al navegador para que renderice todo este contenido.

Sin embargo, ikea, realiza varias llamadas en las renderiza por componente cada sección, fijaos en las llamadas orders, stores, onlineshoppinglist, userinfo, etc.

Vamos con el gráfico:

![Gateway Aggregation](/img/cloudpatterns/gateway-aggregation-pattern.png "Gateway Aggregation")

> Os recomiendo una lectura buscad FAT Client - THIN Server vs THIN Client - FAT Server o también llamado Thin Client vs Fat Client
> Es sobre sistema distribuidos y las aproximaciones.

