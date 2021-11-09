---
layout: post
title: Health Endpoint Monitoring
tags: Arquitectura
---

Health Endpoint Monitoring es un patrón de disponibilidad el cual nos permite verificar la salud de nuestros servicios exponiendo un servicio que monitorizamos cada x tiempo.

Básicamente, lo que hacemos es llamar a un/os servicio/s y que esto/s nos vaya/n respondiendo la pregunta ¿Sigues vivo? (Keep Alive).

![health-endpoint-monitoring](/img/cloudpatterns/health-endpoint-monitoring.png "health-endpoint-monitoring")

Como se puede apreciar en el gráfico, en esta infraestructura se monitorizan tanto los servicios web, los servicios de datos y los servicios background.

Hay que decir que, para este patrón podemos afinar todo lo que necesitemos y que no solo podemos saber el estado del servicio (vivo o muerto), sigo que podemos monitorizar otras métricas como el tiempo de respuesta, validar la respuesta, caducidad de certificados, latencia de DNS, etc...

Finalmente, os dejo un enlace del repositorio de Microsoft, donde implementa este patrón con código [Repo Health EndPoint Monitor](https://github.com/mspnp/cloud-design-patterns/tree/master/health-endpoint-monitoring).

Un saludo.
