---
layout: post
title: Backend for FrontEnds
tags: Arquitectura
---

¡Hola de nuevo! ¡Feliz año a todos! Hoy presentaremos el patrón de implementación Backends para Frontends. Este patrón está basado en el concepto "S" de SOLID de separación de responsabilidades.

Lo que viene a decir es, teniendo una api que es consumida tanto por un aplicación móvil, cómo por una aplicación web deberiamos separar las llamadas que realiza la app mobil de las llamadas que realiza la aplicación web.

Una imagen vale más que mil palabras:

![Backend for Frontend](/img/cloudpatterns/backforfront.png "Backend for Frontend")

Ahora, porqué esta aproximación es mucho mejor y coherente con nuestra infraestructura cloud?

En primer lugar, teniendo separados los servicios, estos se pueden escalar independientemente según su tráfico.

Por otro lado, aunque puedan tener llamadas iguales en nuestras apis, las dimensiones y cantidad de información a mostrar en cada dispositivo es diferente, con lo que nos señala que los modelos a devolver en nuestra llamadas son, en la parte web con muchas más propiedades y en la parte mobile, con muchas menos propiedades. Esta misma simplificación nos ayuda a reducir el peso de las llamadas en nuestros dispositivos móviles.

Un saludos.
