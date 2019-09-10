---
layout: post
title: Health Endpoint Monitoring
tags: Arquitectura
---

Health Endpoint Monitoring es un patrón de disponibilidad el cual nos permite verificar la salud de nuestros servicios exponiendo un servicio que monitorizamos cada x tiempo.

Básicamente, lo que hacemos es llamar a un servicio que nos vaya respondiendo la pregunta ¿Sigues vivo? (Keep Alive).

![health-endpoint-monitoring](/img/cloudpatterns/health-endpoint-monitoring.png "health-endpoint-monitoring")