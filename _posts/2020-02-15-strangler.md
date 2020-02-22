---
layout: post
title: Strangler
tags: Arquitectura
---

Hola a todos, hoy vamos a ver el patrón Strangler o Estrangulamiento. 

![homer strangler bart](/img/cloudpatterns/homerstranglerbart.jpeg "homer strangler bart")

No me he podido resistir...

Venga va, seguimos.

El patrón Strangler es un patrón que nos sirve para ir migradando servicios o aplicaciones que se nos quedan obsoletas hacia nuevas implementaciones. La metáfora del estrangulamiento, es que, en cada iteración vas "estrangulando" más y más la antigua aplicación hasta que ya no queda nada de lo antiguo y lo has migrado hacia la nueva implementación.

El modo en que empleamos este patrón es poniendo delante de la aplicación a migrar un balanceador, en el que vamos balanceando a medida que vamos migrando las llamadas hacia los nuevos servicios o aplicaciones.

Veamos el gráfico:

![Strangler](/img/cloudpatterns/strangler.png "Strangler")

Como se puede apreciar, con Strangler lo que hemos ido haciendo es migrar las Azure Functions que se ejecutaban en nuestra web app hacia servicios de contenedores. De esta forma, para el usuario este cambio de infraestructura ha sido transparente  y hemos podido aplicar los patrones cloud, que hemos ido aprendiendo, sobre nuestra infraestructura sin dejar nunca de dar servicio.

Un saludo.
