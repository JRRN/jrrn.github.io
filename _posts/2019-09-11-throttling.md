---
layout: post
title: Throttling
tags: Arquitectura
---

El patrón Throttling (estrangulamiento) nos permite controlar el consumo de recursos utilizados por una instancia de una aplicación.

Con este control solventamos la necesidad de que nuestro sistema siga funcionando, cuando el escalado no es lo suficientemente rápido aprovisionando, mientras nuestra aplicación recibe una carga masiva de peticiones, evitando una ralentización de nuestro sistema o una denegación de servicio por que el sistema se colapse.

En este punto podríamos aplicar Throttling rechazando a usuarios específicos que realizan muchas peticiones iguales en un periodo corto de tiempo, degradar servicios secundarios que no son tan importantes para nuestra aplicación, ejecutar las acciones prioritarias para el servicio, retrasando las acciones menos prioritarias para su procesamiento cuando la carga sea menor, etc...

Imaginemos que tenemos una instancia de una aplicación:

![sin-Throttling](/img/cloudpatterns/CasoSinThrottling.png "sin-Throttling")

