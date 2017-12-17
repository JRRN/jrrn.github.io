---
layout: post
title: Move me To Azure
tags: Azure
---

Hola de nuevo, cambiando un poco la temática que llevo siguiendo sobre patrones, me gustaría escribir algo que he descubierto y que es una píldora, fácil y rápida.

En [Plain](https://www.plainconcepts.com "Plain Concepts") he estado trabajando en la integración con una herramienta *third party*.

Es una aplicación que se auto instala en el IIS. La problemática que tenía era la forma de migrar ese instalable sobre un servicio App en Azure.

En [Movemetothecloud](https://www.movemetothecloud.net/ "Migración a Azure") encontré la solución. Con un par de siguiente, siguiente, siguiente, había desplegado la aplicación *third party* en un segundos y funcionando correctamente.

![MoveMeToAzure](/img/movemetoazure/MoveMeToAzureCloud.png "MoveMeToAzure")

También, detecta las connectionstrings del web.config, que entiendo que será capaz de desplegar el ServiceApp por un lado en Azure y hacer la referencia sobre la bd a la que apunte el site.

Dejo abierto este post, para su actualización, ya que esto que comento, es el siguiente paso que voy probar.

[Actualizado]

Lo prometido es deuda...

Efectivamente, he podido comprobar que si la solución tiene connectionsstrings en el web.config, estas son detectadas:

![Connectionsstring](/img/movemetoazure/connstrings.png "connstrings")

- *Los nombres de la aplicación y de BDs han sido borrados.*

Seleccionamos la applicación a migrar hacia Azure y las bases de datos que la aplicación usa.

Nos encontraremos con un asistente en el que podremos parametrizar los nombres tanto del servidor sql como de la WebApp y otro parámetros de la máquina, tipo, etc... 

![MigrationDBToAzure](/img/movemetoazure/migrationDBToAzure.png "migrationDBToAzure")

Y ta-chan! Empieza a migrar tanto el site como las bases de datos y TODO su contenido.

Bueno, bonito y barato.

Saludos.