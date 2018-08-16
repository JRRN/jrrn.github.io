---
layout: post
title: Patrón Template Method
tags: Arquitectura
---

El patrón Template Method nos permite definir un esqueleto de métodos abstractos en los que cada clase concreta sobrecargará estos métodos para definir su comportamiento específico y cuya implementación difiera en algunos pasos.

De esta forma, definimos una clase con métodos abstractos como si fuera un contrato o interfaz, y posteriomente definiremos una clase que herede esta superclase y en la que codificaremos cada método con su algoritmo específico.

Una vez más usaremos el ejemplo de los libros y le daremos otra solución al calculo del IVA desde la perspectiva Template Method.

Veamos el ejemplo:

~~~csharp

public abstract class {

}

~~~