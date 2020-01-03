---
layout: post
title: Anti-Corruption Layer
tags: Arquitectura
---

Hola de nuevo. Lo primero, presta mucha atención a este patrón si estáis trabajando con microservicios o con Arquitecturas DDD (Domain Driven Design).

Anti-Corruption Layer nos recomienda crear una capa de aislamiento que permita a los clientes trabajar con sus modelos de negocio y desacoplar estos modelos en nuestra lógica de negocio. Los sistemas se comunican entre ellos mediante los contratos establecidos (interfaces), y anti-corruption layer lo que nos proporciona es una mínima o nula modificación en las aplicaciones conectadas entre los sistemas. Internamente, la capa se traduce en ambas direcciones según sea necesario entre los dos modelos.

Eric Evans, fue el que acuñó este concepto en su libro sobre [DDD](https://dddcommunity.org/book/evans_2003/ "Domain Driven Design").

Así no reinventaremos la rueda y usaremos el ejemplo que usaba en su libro:

Imaginemos que una aplicación depende de Google Calendar para programar y recordar eventos. Para sincronizar los datos desde y hacia Google Calendar, necesitaremos asignar los datos entre los dos sistemas, es decir, nuestra aplicación y Google Calendar. Esto se debe a que los modelos de datos y la estructura serán diferentes en estos sistemas. Con el patrón anti-corruption layer, lo que haremos es usar un proxy/middleware que traduzca los contratos entre Google Calendar y los contratos que usemos en nuestras aplicaciones.

![Anti-Corruption Layer](/img/cloudpatterns/anti-corruption-layer.png "Anti-Corruption Layer")

Un saludo.
