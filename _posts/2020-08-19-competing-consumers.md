---
layout: post
title: Competing Consumers
tags: Arquitectura
---

Hola! Pues venga que volvermos a la carga que tengo en cola, acabar con los patrones cloud y sobre los sistemas distribuidos.

Competing Consumers, este patrón nos ayuda a procesar y a organizar la carga de peticiones en nuestros sistemas.

El problema de no aplicar este patrón es la carga y cantidad de procesamiento que necesitamos simultaneo para poder responder nuestras peticiones de forma óptima. 

Vamos con el ejemplo. Imaginemos que tenemos una web muy famosa de teléfonos, ordenadores, auriculares, tabletas, etc... Se acerca el Black Friday, ese día en que la gente se vuelve loca con "compra", "compra", cómo si estuviera en la bolsa. 

Llegados a este punto, podemos preveer que ese día la carga de transacciones en nuestra base de datos y en nuestra aplicación nos va a hacer daño a nivel de computacional. 

Solución Parche: Tenemos la opción de preparar el sistema para ese día, escalando las máquinas de forma horizontal y vertical, y aguantar de forma estoica a base de pagar el precio de esa infraestructura para ese día. Para algunos según sus arquitecturas, quizá sea la única solución si el negocio se puede permitir esa factura. Para otras aplicaciones más jóvenes, ese gasto puede acarrear otros problemas o simplemente que no se obtenga el visto bueno para darle a la barrita de escalar horizontalmente o al cambio de máquina en el escalado vertical.

Solución Buena: Aplicar Competing Consumers, que más que un patrón es una forma de mitigar este problema. Con Competing Consumers, lo que vamos a hacer es orientar nuestra arquitectura a eventos o mensajes, teniendo una capa más de infraestructura, donde las peticiones se encolaran y se procesaran de forma FIFO (First in First Out) precesandose de forma asincrona y en segundo plano.

Para ello, tenemos varios brokers de mensajes. Personalemente he probado 3, Azure ServiceBus, RabbitMQ y Kafka. Los tres funcionan muy bien, los primeros suplen lo que es una mensajería convencial, mientras que Kafka da esta misma posibildad y tramas más grandes para streaming, por ejemplo. He empezado a ver Azure Event Grid, que es el hermano mayor de Azure Servicebus, pero de momento no entraré a decir nada más que esto.

Entonces, si lo pensaís bien, nos queda una Api, que al llegar una petición envía un evento o mensaje y devuelve un OK o KO dependiendo si ha podido publicar nuestro mensaje en la cola. Debería ser liviano para una Api poder soportar este proceso con muchas peticiones sobre ella. Y por otro lado, tenemos un consumidor, que depende cómo puedo ejecutar todo el procesamiento de las peticiones encoladas de una a una, o a su vez emitir nuevos mensajes para partir más ese proceso, pero aquí tendría sentido introducir una máquina de estados o un patrón state para las diferentes fases del procesado del objeto o petición.

![Competing Consumers](/img/cloudpatterns/competing-consumers.png "Competing Consumers")


Un saludo y hasta la próxima. 

