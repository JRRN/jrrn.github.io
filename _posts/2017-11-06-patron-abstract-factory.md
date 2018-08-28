---
layout: post
title: Patrón Abstract Factory
tags: Arquitectura
---

El patrón **Abstract Factory** proporciona una interfaz para crear familias de objetos relacionados o que dependen entre sí, sin especificar sus clases concretas.

Esto quiere decir, que, por poner un ejemplo, podríamos crear objetos de tipo Books sin tener que definir los tipos de books explícitamente. Mejor con un ejemplo, ¿no?

Tendríamos la clase factoría abstracta Book. Imaginemos que tenemos un sistema de venta de libros. De esta forma tenemos dos tipos de formatos uno de manera física y otro de manera electrónica.

~~~csharp
public class MediaBook : Book
{
    public MediaBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
        : base(titulo, autor, añoPublicacion, formatType) { }

    public override void MostrarCaracteristicas() 
        => Console.WriteLine($"Datos del libro físico:{_titulo} del autor: {_autor} publicado el: {_añoPublicacion} en formato: {_formatType}");
}

public class PaperBook : Book
{
    public PaperBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
        : base(titulo, autor, añoPublicacion, formatType) { }
    public override void MostrarCaracteristicas()
        => Console.WriteLine($"Datos del libro físico: {_titulo} del autor: {_autor} publicado el: {_añoPublicacion} en formato: {_formatType}");
}

public class MediaMagazine : Magazine
{
    public MediaMagazine(string titulo, int añoPublicacion, FormatType formatType) 
        : base(titulo, añoPublicacion, formatType)
    {
    }

    public override void MostrarCaracteristicas() 
        => Console.WriteLine($"Magazine {_titulo} del año {_añoPublicacion} en formato {_formatType} ");
}

public class PaperMagazine :Magazine
{
    public PaperMagazine(string titulo, int añoPublicacion, FormatType formatType) : base(titulo, añoPublicacion, formatType)
    {
    }
    public override void MostrarCaracteristicas() 
        => Console.WriteLine($"Magazine {_titulo} del año {_añoPublicacion} en formato {_formatType} ");
}


public class Factory : IFactory
{
    public Book NewBook(string titulo, string autor, int añoPublicacion, FormatType formatType)
    {
        switch (formatType)
        {
            case FormatType.Media:
                return new MediaBook(titulo, autor, añoPublicacion, formatType);
            case FormatType.Paper:
                return new PaperBook(titulo, autor, añoPublicacion, formatType);
            default:
                throw new ArgumentOutOfRangeException(nameof(formatType), formatType, null);
        }
    }

    public Magazine NewMagazine(string titulo, int añoPublicacion, FormatType formatType)
    {
        switch (formatType)
        {
            case FormatType.Media:
                return new MediaMagazine(titulo, añoPublicacion, formatType);
            case FormatType.Paper:
                return new PaperMagazine(titulo, añoPublicacion, formatType);
            default:
                throw new ArgumentOutOfRangeException(nameof(formatType), formatType, null);
        }
    }
}

public interface IFactory
{
    Book NewBook(string titulo, string autor, int añoPublicacion, FormatType formatType);
    Magazine NewMagazine(string titulo, int añoPublicacion, FormatType formatType);
}
~~~

Hasta aquí tendríamos la implementación solicitada del ejemplo. Pero como siempre, viene el PO y nos dice que ha tenido una grandiosa idea y que también esta pensando en revistas. Con nuestro patrón solo tendríamos que agregar ciertas clases y mantendríamos nuestro principio Abierto-Cerrado Intacto.

~~~csharp
public abstract class Book {
    protected string _titulo;
    protected string _autor;
    protected int _añoPublicacion;
    protected FormatType _formatType;

    protected Book(string titulo, string autor, int añoPublicacion, FormatType formatType)
    {
        _titulo = titulo;
        _autor = autor;
        _añoPublicacion = añoPublicacion;
        _formatType = formatType;
    }

    public abstract void MostrarCaracteristicas();
}

public abstract class Magazine
{
    protected string _titulo;
    protected int _añoPublicacion;
    protected FormatType _formatType;

    protected Magazine(string titulo, int añoPublicacion, FormatType formatType)
    {
        _titulo = titulo;
        _añoPublicacion = añoPublicacion;
        _formatType = formatType;
    }
    public abstract void MostrarCaracteristicas();
}

public enum FormatType
{
    Media,
    Paper
}


~~~

Y finalmente solo tendríamos que agregar a la interfaz los médotos de CreaMagazine:

~~~csharp
public class AbstractFactoryEditorial {
    int nBooks = 3;
    int nMagazines = 2;

    IFactory fabrica  = new Factory();
    AbstractFactoryPattern.Book[] books = new AbstractFactoryPattern.Book[nBooks];
    AbstractFactoryPattern.Magazine[] magazines = new AbstractFactoryPattern.Magazine [nMagazines];

    for (int index = 0; index < nBooks; index++)
    {
        var formatType = index == 0 ? FormatType.Paper : FormatType.Media;
        books[index] = fabrica.NewBook("Papel","Autor", 1980, formatType);
    }

    for (int index = 0; index < nMagazines; index++){
        var formatType = index == 0 ? FormatType.Paper : FormatType.Media;
        magazines[index] = fabrica.NewMagazine("Papel", 1981, formatType);
    }

    foreach (AbstractFactoryPattern.Book book in books)
        book.MostrarCaracteristicas();
    foreach (AbstractFactoryPattern.Magazine magazine in magazines)
        magazine.MostrarCaracteristicas();
}
~~~

Saludos.
