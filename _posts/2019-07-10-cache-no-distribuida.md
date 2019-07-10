---
layout: post
title: Caché no distribuida en Net Core
tags: Code
---

Hola de nuevo, hoy quiero hablaros de la caché no distribuida que nos aporta Net Core y que la carga en memoria.

Este tipo de caché, como redis, memcaché, etc... se diferencia que no es una caché persistida y distribuida. Esto quiere decir que esta caché se crea en memoria y en cada instancia de servidor de la aplicación tenemos una caché diferente.

Para ello, simplemente necesitamos añadir el servicio en la inyección de dependencias y el paquete nuget **Microsoft.Extensions.Caching.Memory**:

~~~csharp
public void ConfigureServices(IServiceCollection services)
{
    ...
    services.AddMemoryCache();
    ...
}
~~~

Inyectado nuestro servicio, ahora ya podemos usar la Interfaz IMemoryCache y generar cachés de nuestros servicios:

~~~csharp
public class NuestroController : Controller
{
    private IMemoryCache _cache;
    private IUserRepository _userRepository;

    public NuestroController(IMemoryCache memoryCache,
                             IUserRepository userRepository)
    {
        _cache = memoryCache;
        _userRepository = userRepository;
    }

    [HttpGet]
    public async Task<IEnumerable<Usuarios>> GetUsersByCountry(string country)
    {
        var cacheKey = $"users-{country}";
        var users =  await _cache._cache.GetOrCreateAsync(cacheKey, entry =>
        {
            return await _userRepository.GetUsersByCountry(country);
        });
        return users;
    }
}
~~~

Y voilá, ya tenemos una caché montada en memoria. La caché que se forma es usuarios por país. Así si en la primera llamada pedidos los usuarios de España, accederemos hasta el repositorio, nos traeremos los datos y en la salida creará una caché con la clase users-es con los usuarios de España. Si volvemos a ejecutar la llamada al controller, la llamada ya no bajará hasta el repository sino que será la caché quien nos devuelva los usuarios. Sin embargo, si solicitamos los usuarios de México, se producirá el acceder al repositorio y generar la caché de usuarios con la clave users-mx.

Vale, ¿que fácil no? Pues la verdad que sí. Decir que la IMemoryCaché se limita por un [algoritmo LRU](https://es.wikipedia.org/wiki/Algoritmo_de_caché) que nos permite usar el 20% de la RAM de la instancia como máximo.

Este tipo de caché funciona hasta que se llena. Es decir si no liamos a pedir usuarios de países se generaran tantas cachekeys como nos quepan en ese 20%. Las demás irán a repositorio mientras no entre a funcionar el algoritmo LRU.

Ooooooooh!!! Pero tranquis, que es configurable.

Seteamos la vida de la caché, FromSeconds; FromMinutes...:

~~~csharp
var users =  await _cache._cache.GetOrCreateAsync(cacheKey, entry =>
{
    entry.SlidingExpiration = TimeSpan.FromMinutes(60);
    return await _userRepository.GetUsersByCountry(country);
});
~~~

Seteamos la capacidad de la caché a 50 megas **ojito con los cálculos a ojo cubero que nos podemos comer la memoria si nuestro equipo empieza a crear caches en los diferentes servicios sin control**:

~~~csharp
var users =  await _cache._cache.GetOrCreateAsync(cacheKey, entry =>
{
    entry.Size = 50;
    return await _userRepository.GetUsersByCountry(country);
});
~~~

Y de momento eso es todo.

Un saludo y hasta la próxima.