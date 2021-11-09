---
layout: post
title: Gateway Routing
tags: Arquitectura
---

¡Hola! Vamos con el patrón Gateway Routing, este sí que es el famoso gateway que muchos de vosotros conocéis. Simplemente lo que infiere este patrón es centralizar todas las llamadas en un único punto de acceso, donde posterior e internamente se redirigirán al servicio al que se haya realizado la petición.

Para este patrón, aunque tengo un compañero de profesión que no le gusta mucho, os recomiendo la lectura de [Refit](refit "Refit"), ya que nos permite de una manera muy sencilla implementar las llamadas a los servicios desde el gateway sin tener que sudar mucho, a parte, de permitirnos implementar los patrones de [Throttling](throttling "Throttling"), Circuit Breaker y Retry, estos dos últimos los veremos más adelante, de una forma muy sencilla.

Su funcionamiento es cómo funciona un reverse proxy (NGINX). Qué es, que un servidor se hace cargo de las solicitudes procedentes de Internet y las transmite a un servidor backend en segundo plano, dándole y centralizando la seguridad en un punto.

Hay que tener en cuenta que todo el tráfico de nuestra aplicación pasará por este punto, así que tened presente que debe aguantar carros y carretas.

![Gateway Routing](/img/cloudpatterns/gateway_routing.png "Gateway Routing")

Un saludo y hasta la próxima.
