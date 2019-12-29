---
layout: post
title: Ambassador
tags: Arquitectura
---

Hola! El patrón Ambassador nos sirve para colocar antes de otros servicios un "proxy" que nos de más control de comunicaciones sobre estas aplicaciones de terceros, pudiendo aplicar muchos de los patrones que estamos aprendiendo.

Pongamos el caso, tenemos un servicio que nos devuelve las facturas de un usuario. Sin embargo, este servicio se codificó junto a las tablas de Moisés. Cada vez que abrimos ese código, en el caso de tenerlo, pensamos que lo mejor es rehacerlo porque no hay por donde meterle mano. Sin embargo, funciona tan bien que seguimos la regla "no sé cómo lo hace pero funciona, ni lo mires". Sin embargo, necesitamos aplicar los patrones de valet key, throttling, circuit breaker y alguno más para adaptarnos a nuestra infraestructura.

En este momento, entraría en juego nuestro patrón Ambassador, donde colocariamos un un servicio Proxy/Middleware entre el servicio de factoras y nuestra aplicaciones, donde, este middleware tendría aplicadas todas estas soluciones que presentábamos.

![Ambassador](/img/cloudpatterns/ambassador.png "Ambasaddor")

Saludos y hasta la próxima.
