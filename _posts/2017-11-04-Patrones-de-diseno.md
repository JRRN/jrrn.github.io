---
layout: post
title: Patrones de diseño
tags: Arquitectura
---

En este artículo introductorio, que formará parte de una serie de artículos breves, revisaremos los patrones de diseño disponibles para C# y otros lenguajes de programación.

Mi intención es explicar todos los patrones de una forma clara, con ejemplos y con su codificación y de paso aprender los que no he usado.

Los patrones de diseño nos sirven para abstraer lógicas de programación sobre paradigmas conocidos.

En definitiva, esto significa que si por ejemplo tomásemos como paradigma un blog. Usaríamos una template (patrón) sobre todas las páginas que fueran de tipo blogPage y/u otra template (patrón)  para las páginas de tipo HomePage.

Así, pasamos a enumerar los patrones que revisaremos en esta serie de artículos:

### Patrones de construcción ###

Los patrones de construcción tienen como misión abstraer los mecanimos de creación de objetos, volviendose independiente de la forma en que se crean los objetos y los mecanismos de instanciación de las clases concretas.

Estos patrones encapsulan el uso de clases concretas y favorecen el uso de interfaces en las relaciones con los objectos, posibilitando una mayor abstracción en el diseño global.

- [Patrón Abstract Factory](patron-abstract-factory "Patrón Abstract Factory")
- [Patrón Builder](patron-builder "Patrón Builder")
- [Patrón Factory Method](patron-factory-method "Patrón Factory Method")
- [Patrón Prototype](patron-prototype "Patrón Prototype")
- [Patrón Singleton](patron-singleton "Patrón Singleton")

### Patrones de estructura ###

- Patrón Adapter
- Patrón Bridge
- Patrón Composite
- Patrón Decorator
- Patrón Facade
- Patrón Flyweight
- Patrón Proxy

### Patrones de comportamiento ###

- Patrón Chain of Responsibility
- Patrón Command
- Patrón Interpreter
- Patrón Iterator
- Patrón Mediator
- Patrón Memento
- Patrón Observer
- Patrón State
- Patrón Strategy
- Patrón Template Method
- Patrón Visitor

Nos vemos en el siguiente post.