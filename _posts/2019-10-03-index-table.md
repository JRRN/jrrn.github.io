---
layout: post
title: Index Table
tags: Arquitectura
---

El patrón Index Table se utiliza para crear índices secundarios sobre consultas, que la aplicación necesita, en campos que no son una primary key y así tener un acceso a los datos con una aceptable optimización.

Situémonos, tenemos una tabla de productos, donde como es habitual, tenemos un id_producto como primary key, el campo nombre de producto, el tipo de producto y el precio.

|(*) id_producto|producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|1|Patatas|1| 2|
|2|Zanahorias|1|3|
|3|Carne|2|6|
|4|Pescado|3|5|
|5|Plátanos|4|3|

\* Primary Key

En nuestra aplicación para buscar patatas ejecutaríamos la query:

    SELECT * from TABLE Where id_producto = 1

Con lo que obtendríamos con un buen rendimiento:

|(*) id_producto|producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|1|Patatas|1| 2|

Sin embargo, no siempre tenemos porque conocer el identificador de lo que estamos buscando en base de datos y esto nos penaliza si buscamos por "Patatas".

    SELECT * from TABLE Where producto = "Patatas"

A pesar de que lo encuentra, si tuviéramos una base de datos con bastante peso, esta query podría penalizar al rendimiento de la aplicación o incluso darnos un timeout en la query, cosa que no sería necesario si implementáramos Index Table.

Aunque existen motores de bases de datos, SQL Server lo permite, en los que puedes crear índices secundarios, puede ser una buena práctica no crear estos índices y usar este patrón. Por otro lado, para aquellos motores NO-SQL en los que los índices "no existen" (lo pongo entre comillas antes de que os tiréis al cuello) este patrón se ajusta bastante bien.

Al lío.

Tenemos varias estrategias según cuantos índices secundarios necesitamos:

La primera de ellas (romper la 1ª Forma Normal, 2ªFN, 3ªFN ...), recomendable cuando nuestros datos no se actualizan con frecuencia, duplicando la tabla pero cambiando la primary key:

|(*) producto|id_producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|Patatas|1|1| 2|
|Zanahorias|2|1|3|
|Carne|3|2|6|
|Pescado|4|3|5|
|Plátanos|5|4|3|

Si volviéramos a ejecutar la consulta:

    SELECT * from TABLE_PRODUCT_NAME Where producto = "Patatas"

El rendimiento de nuestra query estaría optimizado.

La segunda estrategia sería crear tablas con referencias a otras tablas formalizadas con los índices secundarios. Más vale un a imagen que mil palabras:

|(*) id_producto|producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|1|Patatas|1| 2|
|2|Zanahorias|1|3|
|3|Carne|2|6|
|4|Pescado|3|5|
|5|Plátanos|4|3|

relación (*)id_producto = id_producto

|(*) producto|id_producto|
|:-:|:-:|
|Patatas|1|
|Zanahorias|2|
|Carne|3|
|Pescado|4|
|Plátanos|5|

De esta forma si quisiéramos obtener el precio de las patatas:

    @Id = SELECT id  from TABLE_PRODUCTS_NAME WHERE producto = "Patatas"
    SELECT prices from TABLE_PRODUCTS WHERE id = "@Id"

Lo malo, sí, como vemos tenemos que tirar dos queries. ¿¿Y la JOIN?? Pensad en grandes bases de datos...

La tercera estrategía, es una mezcla entre la primera y la segunda, es decir, duplicar... las tablas normalizadas pero con los índices que queramos y en función de la SELECT hacer un switch a la tabla que contiene el índice por el WHERE que estamos buscando:


TABLE PRIMARY KEY PRODUCT_ID
|(*) id_producto|producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|1|Patatas|1| 2|
|2|Zanahorias|1|3|
|3|Carne|2|6|
|4|Pescado|3|5|
|5|Plátanos|4|3|

TABLE PRIMARY KEY PRODUCT_NAME
|(*) producto|id_producto|tipo_producto|precio|
|:-:|:-:|:-:|:-:|
|Patatas|1|1| 2|
|Zanahorias|2|1|3|
|Carne|3|2|6|
|Pescado|4|3|5|
|Plátanos|5|4|3|

Que buscamos "Patatas" pues atacamos a TABLE PRIMARY KEY PRODUCT_NAME, en cambio si buscamos por id atacaremos a TABLE PRIMARY KEY PRODUCT_ID.

> Si buscáramos por nombre de producto y por tipo de producto una solución es crear una tabla concatenado los estos parámetros como clave primaria en la tabla resultante TABLE PRIMARY KEY PRODUCT_NAME+PRODUCT_TYPE.

Un saludo.
