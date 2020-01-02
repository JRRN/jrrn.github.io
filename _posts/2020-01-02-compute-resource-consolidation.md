---
layout: post
title: Compute Resource Consolidation
tags: Arquitectura
---

Buenas!! Compute Resource Consolidation es un patrón de implementación que nos ayuda, aunque hay que tener muy clara la foto de nuestro aprovisionamiento en el Cloud, a optimizar nuestra infraestructura en términos de costes y unidades de proceso.

Lo que viene a decir es que donde caben 2, caben 3.

Imaginemos que tenemos varias APIS en nuestra arquitectura. La API-diurna de consumo de nuestra aplicación que tiene su mayor carga en un horario diurno, pongamos de 8 a 22. La API-nocturna que es consumida por procesos background para cálculos, movimientos de datos, generación de informes y que principalmente tiene un horario de ejecución de 0 a 6. Y finalmente la API-notificaciones, con un 24x7, que es una API que recibe llamadas para comunicar notificaciones vía mail tanto de usuarios, como del estado de finalización de nuestros procesos nocturnos.

La primera implementación de nuestra infraestructura podría ser tener 3 App Services para cada uno de nuestros servicios:

![Bad Compute Resource Consolidation](/img/cloudpatterns/bad_compute_resource_consolidation.png "Bad Compute Resource Consolidation")

Y aunque no es mala idea, porque la escalabilidad sería independiente. Es cierto que pagamos por tres App Services, se usen o no se usen.

Así, aplicando el patrón y con la información que tenemos de como se encuentra implementada nuestra arquitectura, la solución sería:

![Good Compute Resource Consolidation](/img/cloudpatterns/good_compute_resource_consolidation.png "Good Compute Resource Consolidation")

Sí. Unificariamos los servicios de API Diurna y API Nocturna en un mismo App Service Plan y dejaríamos la API Notificaciones en otro App Service Plan por separado.

¿Por qué? Los nombres y lo horarios son la pista... Porqué mientras la API diurna está a pleno rendimiento la nocturna descansa, y mientras que la nocturna trabaja la diurna descansa. De esta forma el App Service Plan esta amortizado ya que trabaja a pleno rendimiento casi las 24 horas del día y además reducimos los costes, ya que pasamos de 3 a 2 App Service Plans.

> Este patrón es aplicable a Cloud Services, App Services y Virtual Machines, con todas las tecnologías que abarcan estos servicios. Ni se os ocurra aplicarlo a código, hacerlo implicaría volver a los monolitos.

Sin más, un saludo.