---
layout: post
title: Claim-Check
tags: Arquitectura
---

Hola de nuevo.

Antes de describir el patrón, quiero hacer una introducción a los servicios de mensajería para entender porque existe este patrón.

Como sabréis, existen servicios de mensajería como Azure ServiceBus, Azure Event Grid, RabbitMQ, Apache Kakfa, etc... Estos servicios nos ayudan a comunicar, enrutando las tramas de mensajes, entre los diferentes sistemas distribuidos que tengamos en nuestra infraestructura. 

Como todo, tenemos ciertas limitaciones en este tipo de mensajes. En la que nos ayuda Claim Check es en el peso de los mensajes. [ServiceBus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted#capacity-and-quotas "ServiceBus") por ejemplo, dependiendo si usamos colas, topics tiene un límite de mensajes de entre 64kb a 1Mb, dependiendo de la tier que nos decidamos a pagar. RabbitMQ por el contrario, alcanza los 2GB de tamaño de mensajes, aunque me parece una locura admitir estos tamaños ya que se nos puede ir de las manos e imaginaos Amazon enviando en su sistema mensajes de 2GB, que espacio necesitaría ¿¿¿¿???? 

Pues bien, Claim-Check nos permite jugar con esta limitación y optimizar un poco nuestro sistema distribuido sin perder la eficiencia de la mensajería.

Así, para implementar este patrón, lo que haremos será almacenar en un contexto persistente la información y pasar por el mensaje la referencia del identificador que apunta al contexto de persistencia.   

El receptor del mensaje, lo que hará será recibir el identificar e ir a buscar al contexto de persistencia la información almacenada.

Vamos con el ejemplo, que así lo entenderemos mejor y más rápido.

Imaginaos que mi hermano, me quiere enviar 150 Mb de fotos de mi sobrina ahora en Carnaval por correo. Gmail o Outlook le va a decir que nanai de la china, que no puede enviar un mail de 150 MB, que si quiere se lo sube a Google Drive/OneDrive y luego me manda el link de la carpeta de Google Drive/OneDrive y yo ya accedo a las fotos.

Ala, ahí tenéis el patrón descrito y como deberiamos implementarlo.

Almacenariamos el contenido del mensaje en un CosmosDb/SQL Server/Storage y mandariamos la el id/Url para que el receptor vaya a buscar el contenido a CosmosDb/SQL Server/Storage.

![Claim Check](/img/cloudpatterns/claim-check.png "Claim Check")

Un saludo y hasta la próxima.
