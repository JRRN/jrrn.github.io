---
layout: post
title: Caché no distribuida en Net Core
tags: Code
---

Hola de nuevo, hoy quiero hablaros de la caché no distribuida que nos aporta Net Core y que la carga en memoria.

Este tipo de caché, como redis, memcaché, etc... se diferencia que no es una caché persistida y distribuida. Esto quiere decir que esta caché se crea en memoria y en cada instancia de servidor de la aplicación tenemos una caché diferente.

Para ello, simplemente necesitamos añadir el servicio en la injección de dependencias:

~~~csharp
public void ConfigureServices(IServiceCollection services)
{
    ...
    services.AddMemoryCache();
    ...
}
~~~
