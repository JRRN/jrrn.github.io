---
layout: post
title: Scheduler Agent Supervisor
tags: Arquitectura
---

El patrón Scheduler Agent Supervisor nos sirve para realizar varias operaciones y coordinarlas cómo si se tratase de una única operación. De esta forma, si se produce un error en algunas de las sub operaciones, es capaz de compensar las sub operaciones ya ejecutadas o controlar y lanzar una excepción de conjunto, tratando de volver a ejecutar las operaciones fallidas o en su defecto deshacer el camino ya transitado.

Si echamos la vista atrás y repasamos los patrones de diseño, y nos situamos en los patrones de comportamiento, podremos encontrar cierta similitud al [Patrón State](patron-state "Patrón State"). El concepto es parecido, pero aplicado a sistemas distribuidos, donde en el patrón state trabajábamos con un objeto y en el Scheduler Agent Supervisor trabajamos con sistemas aplicaciones distribuidas. Aunque no funcionan de la misma manera, el concepto es parecido y nos sirve para tener una idea de por donde van los tiros.

Entonces la manera de implementar este patrón es mediante actores, donde cada actor tiene su papel dentro de la arquitectura. Tendremos un actor principal (Scheduler) que será un orquestador de todos los procesos (Agentes), que se encargará de mantener un estado de las peticiones y finalmente tendremos un actor que realiza las tareas de validación (Supervisor) que se encargará de controlar las respuestas de cada una de las operaciones, tanto si han ido bien, cómo si han ido mal. Y este será el principal encargado de orquestar los reintentos o las compensaciones.

![Scheduler Agent Supervisor](/img/cloudpatterns/scheduler-agent-supervisor.png "Scheduler Agent Supervisor")

Un saludo y hasta la próxima.

