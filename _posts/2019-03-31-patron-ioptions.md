---
layout: post
title: Patrón de Opciones
tags: Arquitectura
---

¿Quien no recuerda los maravillosos Configuration Provider que nos hemos montado más de una vez para albergar en un clase todas las settings de nuestra aplicación y no tener desparramado por el código el acceso a estas (de esta forma, si cambiaba una setting se centralizaba en un punto y se replicaba en todo el contexto de la aplicación)?

¿Qué no sabes de lo que te hablo?:

~~~csharp
public static class ConfigProvider {  
    public string Usuario = ConfigurationManager.AppSettings["User"];
    public string Password = ConfigurationManager.AppSettings["Password"];
    public int Reintentos = 3;
    public bool IsLoginActive = true;

    etc.
    etc.
    etc.            
}

public static class Main {
    var config = new ConfigProvider();

    Console.WriteLine(config.Usuario);
}
~~~

Sin embargo, con Net Core, se lo han currado un poco más y ahora queda centralizado a la hora de registrar la dependencias.

Primero de todo generamos una clase para la sección de las appsettings o para todo el appsettings, recordemos que si hacemos esta última, será accesible desde cualquier punto de la aplicación.

Appsettings.json
{
  "MySettings": {
    "StringSetting": "My Value",
    "IntSetting": 23
  }
}

~~~csharp
public class MySettings
{
    public string StringSetting { get; set; }
    public int IntSetting { get; set; }
}
~~~

Por otro lado registramos en el contenedor de servicios la clase que hemos definido anteriormente, aquí esta la magia:

~~~csharp
    services.Configure<MySettings>(
        options => Configuration.GetSection("MySettings")
        .Bind(options));
~~~

En este punto al levantar la aplicación ésta gestiona el contenedor de dependencias y lee el archivo appsettings registrando una instancia de la clase MySettings.

Y ya.

A partir de aquí en las clases que necesitemos acceder a la configuración simplemente inyectaremos una interfaz IOptions<MySettings> y podremos acceder al servicio que se registro en el contenedor de dependencias:

~~~csharp
public class HomeController : Controller
{
    private MySettings _settings;
    public HomeController(IOptions<MySettings> settings)
    {
        _settings = settings.Value
        // _settings.StringSetting == "My Value";
    }
}
~~~

Lo mejor de todo es que podemos inyectar esta configuración en páginas razor:

~~~csharp
@page
@model IndexModel
@using Microsoft.Extensions.Options
@inject IOptionsMonitor<MySettings> _settings
@{
    ViewData["StringSetting"] = _settings.StringSetting;
}

<h1>@ViewData["StringSetting"]</h1>
~~~

Saludos.