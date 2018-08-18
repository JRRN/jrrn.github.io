---
layout: post
title: Patrón Abstract Factory
tags: Arquitectura
---

El patrón **Abstract Factory** proporciona una interfaz para crear familias de objetos relacionados o que dependen entre sí, sin especificar sus clases concretas.

Esto quiere decir, que, por poner un ejemplo, podríamos crear objetos de tipo Books sin tener que definir los tipos de books explícitamente. Mejor con un ejemplo, ¿no?

Tendríamos la clase factoría abstracta Book. Imaginemos que tenemos un sistema de venta de libros. De esta forma tenemos dos tipos de formatos uno de manera física y otro de manera electrónica.

~~~csharp
public class PaperBook :  Book {
    public PaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
    : base(titulo, autor, añoPublicacion, formatType) { }
    public override void mostrarCaracteristicas() {
        Console.WriteLine($"Datos del libro físico: {titulo} del autor: {autor} publicado el: {añoPublicacion} en formato: {formatype}");
    }
}

public class MediaBook: Book {
    public PaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
    : base(titulo, autor, añoPublicacion, formatType) {}

    public override void mostrarCaracteristicas() {
        Console.WriteLine($"Datos del libro físico:{titulo} del autor: {autor} publicado el: {añoPublicacion} en formato: {formatype}");
    }
}

public interface GenerateBook {
    PaperBook creaPaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType);

    MediaBook creaMediaBook (string titulo, string autor, int añoPublicacion, FormatType formatType);
}

public class GeneratePaperBook: GenerateBook {
    public PaperBook creaPaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
    {
        return new PaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType);
    }
}

public class GenerateMediaBook: GenerateBook {
    public MediaBook creaMediaBook(string titulo, string autor, int añoPublicacion, FormatType formatType) {
        return new MediaBook(string titulo, string autor, int añoPublicacion, FormatType formatType);
    }
}
~~~

Hasta aquí tendríamos la implementación solicitada del ejemplo. Pero como siempre, viene el PO y nos dice que ha tenido una grandiosa idea y que también esta pensando en revistas. Con nuestro patrón solo tendríamos que agregar ciertas clases y mantendríamos nuestro principio Abierto-Cerrado Intacto.

~~~csharp
public abstract class Book {
    protected string _titulo;
    protected string _autor;
    protected int _añoPublicacion;
    protected FormatType _formatType;
    public Magazine(string titulo, string autor, int añoPublicacion, FormatType formatType) {
        _titulo = titulo;
        _autor = autor;
        _añoPublicacion = añoPublicacion;
        _formatType = formatType;
    }

    public abstract void mostrarCaracteristicas();
}

public class PaperMagazine: Book {
    public PaperMagazine(string titulo, string autor, int añoPublicacion, FormatType formatType)
    : base(titulo, autor, añoPublicacion, formatType){}

    public override void mostrarCaracteristicas() {
        Console.WriteLine($"Datos de la Revista física: {titulo} del autor: {autor} publicada el: {añoPublicacion} de formato: {formatype}");
    }
}

public class MediaMagazine: Book {
    public MediaMagazine(string titulo, string autor, int añoPublicacion, FormatType formatType)
    : base(titulo, autor, añoPublicacion, formatType){}
    public override void mostrarCaracteristicas() {
        Console.WriteLine($"Datos de la Revista Electrónica: {titulo} del autor: {autor} publicada el: {añoPublicacion} de formato: {formatype}");
    }
}
~~~

Y finalmente solo tendríamos que agregar a la interfaz los médotos de CreaMagazine:

~~~csharp
public interface AbstractFactoryEditorial {
    PaperBook creaPaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType);
    MediaBook creaMediaBook (string titulo, string autor, int añoPublicacion, FormatType formatType);
    PaperMagazine creaPaperMagazine (string titulo, string autor, int añoPublicacion, FormatType formatType);
    MediaMagazine creaMediaMagazine (string titulo, string autor, int añoPublicacion, FormatType formatType);
}
~~~

Saludos.
