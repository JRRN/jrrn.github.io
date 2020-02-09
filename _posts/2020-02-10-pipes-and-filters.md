---
layout: post
title: Pipes And Filters
tags: Arquitectura
---

Hola a todos, uno más; Pipes and Filters.

Pipes and filters nos recomienda intentar llevar las operaciones de nuestra arquitectura a unidades atómicas, lo cual no permite, poder tener una mayor flexibilidad con estas unidades y mirando hacia la infraestructura nos da un mayor control sobre esta.

La idea es aplicar la ["S"](solid "Solid") de solid (Single Responsability) pero a nuestra infraestructura.

Vamos con el ejemplo.

Imaginemos que tenemos un servicio el cual debe ejecutar varias acciones en un flujo. Introducimos un texto y queremos traducirlo a diferentes idiomas. Nuestro código podría ser:

~~~csharp
public Task WorkFlowTranslate(string inputText) {
    foreach(var languages in _languages){
        var textTranslated = await _translationService.Translate(inputText, language);
        await _saveDataService.Save(textTranslated, language);
    }
}
~~~

Como vemos no tiene magia, recibimos un parámetro string a traducir, recorremos el diccionario de idiomas, llamamos al servicio de traducción y persistimos en el contexto de base de datos.

Veamos, como aplicar el patrón pipes and filters para mejorar el rendimiento y la escalabilidad de este sencillo código:

![Pipes And Filters](/img/cloudpatterns/pipes_filters_simple.png "Pipes And Filters")

Vale, pues ya tenemos traducido nuestro código a infraestructura como nos dice el patrón.

Veamos las ventajas, la primera son las dependencias, cada componente conoce solo lo que debe hacer y no tiene referencias con otros servicios, entre un mensaje, sale un "mensaje". Lo segundo es la escalabilidad, si el servicio de traducciones chinas, se engancha por aquello de traducir palabras a símbolos, sabremos que escalará solo el servicio de traducciones chinas. Tercero la reutilización de código, ¿creéis que hay diferencias entre los servicios de traducciones o son el mismo? Y finalmente, la modularidad, que la veremos con un ejemplo más. ¿Que pasaría si quisiéramos a nuestro flujo agregar un servicio de correción del texto introducido? :yum:

![Pipes And Filters Add Pipe](/img/cloudpatterns/pipes_filters_add.png "Pipes And Filters Add Pipe")

Pues efectivamente, sería tan fácil como cambiar la publicación de los mensajes y redirigirlos a una nueva cola, que los interceptara en el servicio corrector, corrigiera los textos de entrada y publicara los mensajes en las colas de traducciones.

De aquí el nombre de la parte de pipes del patrón.

¿Rafa y la parte de filters? Sí, sí, son pipes pero de agregados, los filters se usan en esta arquitectura para tratar, convertir, extraer, excluir... datos de las salidas que produce cada pipe.

Un saludo y hasta la próxima.