---
layout: post
title: Principios KISS - DRY - YAGNI - Red Green Refactor
tags: Arquitectura
---

Hola de nuevo, para acabar una más de principios para el diseño de software:

<br>

**KISS** - (Mantenlo simple, estúpido): Esto es algo que se explica por sí mismo: siempre es más fácil evitar errores, mejorar el rendimiento, agregar funciones y mantener un software más simple que algo complicado. Y como en la vida, las cosas simples y no forzadas mejor...

Este principio no significa que nunca se deba introducir complejidad para resolver un problema complejo, significa que debemos usar la solución más simple para poder resolverlo.

<br>

**DRY** (No se repita): **DRY** es algo menos explícito que **KISS**, pero tiene sentido una vez que lo piensas. 

Una fuente común de errores es el código repetido que hace cosas muy similares. Los errores se introducen en los sistemas como código repetido cuando se agrega una nueva funcionalidad y solo se actualiza en una de las dos partes de código similar.

Peor aún peor, si hay un error existente, es posible que solo se solucione en un lado, lo que hace que el error se vuelva a abrir debido a la corrección incompleta.

<br>

**YAGNI** (No lo voy a necesitar): otra fuente común de errores es el código escrito "porque podríamos necesitarlo algún día" o en "creo que lo usaremos más adelante".

Al aplicar **YAGNI**, puede ayudar a **KISS**. Con **YAGNI** puedes ir un poco más lejos, por ejemplo, escribiendo un sistema que solo se adapte a la cantidad exacta de usuarios que tiene hoy.

En general, el desarrollo de cualquier funcionalidad basada en la especulación es una bomba que tarde o temprano estallará. El riesgo siempre debe ser considerado cuidadosamente antes de seguir.

<br>

**Rojo, verde, refactor**: Este concepto proviene de la comunidad TDD.

La idea es que cualquier unidad de código en la que se esté trabajando debe pasar por tres fases principales:

- **Rojo**: Primero, no hace lo que debe, ya sea porque no tiene la función deseada, tiene un error no deseado o simplemente no existe. Esto se puede verificar a través de pruebas automáticas o manuales, o analizando el código existente.

- **Verde**: A continuación, hacemos que el código funcione según lo previsto y se verifica que funciona de la misma manera que se verificó el estado original en el que no funcionaba.

- **Refactor**: Ahora que el código funciona según lo previsto, se debe invertir tiempo para asegurar que el código esté bien factorizado y que cumple la nueva funcionalidad, verificando que tanto la funcionalidad anterior como la nueva funcionalidad continúen dando un resultado esperado.

<br>
Finalmente:

**Red Green Refactor** ayuda a los desarrolladores a aplicar todos los principios de la escritura de un buen software al ayudar a la comprensión del problema en cuestión, creando una solución **KISS** sin romper la funcionalidad existente -> **YAGNI**, y garantizar que el código resultante esté listo para realizar cambios futuros -> **DRY**.

Saludos.
