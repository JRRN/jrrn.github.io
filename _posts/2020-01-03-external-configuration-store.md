---
layout: post
title: External Configuration Store
tags: Arquitectura
---

!Hola de nuevo! Seguimos con este patrón de implementación, el cual nos dice que deberíamos tener centralizada todas las configuraciones en un punto y consumirlas desde todos los servicios que expongamos.

En Azure, hasta hace poco teníamos el servicio App Configuration en modo preview, desde hace un tiempo, ya podemos usar este recurso que nos ayuda a implementar este patrón y del que hablaremos en otro momento ya que nos da muchas posibilidades.

Hasta ahora, normalmente, teníamos nuestras settings en los archivos appsettings.json/web.config/App.config de nuestras aplicaciones, donde almacenábamos todo aquello necesario para que la aplicación funcionara e interactuara con las bases de datos, con otras APIS o con cualquier recurso o servicio ajeno al contexto de esa aplicación.

El concepto en el que se basa este patrón es muy parecido, pero llevado a gran escala, al patrón [IOptions](patron-ioptions "IOptions") que explicamos anteriormente.

En este caso tendríamos una API que sirve las settings de configuración a nuestros servicios. De esta forma si tuviéramos que cambiar una cadena de conexión, no tendríamos que recorrernos todas las aplicaciones, substituir esta cadena y redesplegar.

Vamos con el esquema gráfico:

![External Configuration Store](/img/cloudpatterns/external_configuration_store.png "External Configuration Store")

Saludos.