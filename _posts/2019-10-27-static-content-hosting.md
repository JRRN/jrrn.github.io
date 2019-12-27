---
layout: post
title: Static Content Hosting
tags: Arquitectura
---

El objetivo de este patrón es reducir el coste de llamadas que no necesiten pasar por una lógica o servicio devolviendo el contenido o recurso requerido de la forma más rápida posible.

Imaginemos que nuestra web tiene varios documentos PDF donde le explicamos al usuario como vamos a tratar su datos mientras los stalkeamos en su navegación por el site. Podríamos pensar que, cuando el usuario inicia esta solicitud, nos llama a la controller, voy al servicio que devuelve el contenido del pdf en base64 y que el navegador renderiza por las cabeceras en una nueva tab como pdf. Sí, ¿no? Pues no, justamente este patrón lo que nos recomienda es que le devolvamos el pdf desde la url del storage que apunta al pdf de gestion_datos.pdf.

De esta forma, reducimos el procesamiento en nuestra/s instancia/s, que valen dinerito y usamos un storage que es más baratito.

El truco, es pensar en este tipo de contenido y en su viabilidad de si sería aconsejable meterlo en un cdn.

Saludos y hasta la próxima.
