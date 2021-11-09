---
layout: post
title: Throttling
tags: Arquitectura
---

El patrón Throttling (estrangulamiento) nos permite controlar el consumo de recursos utilizados por una instancia de una aplicación.

Con este control solventamos la necesidad de que nuestro sistema siga funcionando, cuando el escalado no es lo suficientemente rápido aprovisionando, mientras nuestra aplicación recibe una carga masiva de peticiones, evitando una ralentización de nuestro sistema o una denegación de servicio por que el sistema se colapse.

En este punto podríamos aplicar Throttling rechazando a usuarios específicos que realizan muchas peticiones iguales en un periodo corto de tiempo, degradar servicios secundarios que no son tan importantes para nuestra aplicación, ejecutar las acciones prioritarias para el servicio, retrasando las acciones menos prioritarias para su procesamiento cuando la carga sea menor, etc...

Imaginemos que tenemos una instancia de una aplicación:

Supongamos también que nuestra aplicación tiene un limite de 150 peticiones antes de que lleguemos al colapso del servidor y que somos capaces de procesar 50 peticiones en una unidad de tiempo. En la tabla siguiente podemos ver como el proceso A llegado al t3 se colapsa y pone en peligro nuestra aplicación pudiendo perjudicar a los procesos B y procesos C que están correctamente escalados.

![sin-Throttling](/img/cloudpatterns/CasoSinThrottling.png "sin-Throttling")

Con Throttling lo que podríamos hacer es utilizar la estrategia de procesamiento de 50 peticiones de los procesos B y C para reducir la carga de A, no colapsar el servidor y esperar a que el aprovisionamiento del escalado llegue a tiempo antes de una caiga de todo el sistema.

Veamos como simularíamos la misma tabla, pero con Throttling:

![con-Throttling](/img/cloudpatterns/CasoConThrottling.png "con-Throttling")

Como podemos ver, incluso si aplicamos la estrategia de estrangular los procesos B y C en ciertos tiempos, no tendríamos la necesidad de escalar la máquina porque esta es capaz de satisfacer todas las peticiones de una forma liviana.

Saludos y hasta la próxima.
