---
layout: post
title: Patrón Chain of Responsability
tags: Arquitectura
---
El patrón **Chain Of Responsability** nos ayuda a crear una secuencia de unión entre objetos tal que, si el objeto más interno de la cadena no es capaz de dar una respuesta, uno de los objetos de nivel superior será el encargado de darla. Esta respuesta será a nivel del contexto en que el objeto se encuentre y sea capaz de responder.

Como siempre, mejor con un ejemplo, ¿no?

Os acordáis de nuestro ejemplo de venta de libros...

En él, tenemos libros, dentro de libros tenemos categoría de libros y dentro de la categoría de libros tenemos el libro en cuestión.

Empezamos:

~~~csharp
public abstract class BaseLibro {
    public BaseLibro siguiente { protected get; set; }

    private string DescripcionBase() => "Descripción base : Es un libro.";

    protected abstract string descripcion { get; }

    public string GetDescripcion()
    {
        var result = descripcion;

        if (result != null)
        {
            return result;
        }
        return siguiente != null ? siguiente.GetDescripcion() : DescripcionBase();
    }
}

public class LibroCoR : BaseLibro
{
    protected string _libroDescripcion;

    public LibroCoR(string descripcion)
    {
        _libroDescripcion = descripcion;
    }

    protected override string descripcion => _libroDescripcion;
}

public class LibroCategoriaDescripcion : BaseLibro {
        protected string _categoriaDescripcion;
        protected string _categoria;

        public LibroCategoriaDescripcion(string descripcion, string categoria)
        {
            _categoriaDescripcion = descripcion;
            _categoria = categoria;
        }

        protected override string descripcion => 
                _categoriaDescripcion != null ? $"La categoria {_categoria} 
                : {_categoriaDescripcion}" : null;
}

public class LibroDescripcion : BaseLibro {
        protected string _libroDescripcion;
        protected string _libro;

        public LibroDescripcion(string descripcion, string libro)
        {
            _libroDescripcion = descripcion;
            _libro = libro;
        }

        protected override string descripcion => 
            _libroDescripcion != null ? $"El libro {_libro} 
            : {_libroDescripcion}" : null;
}

public static void Show()
{
    BaseLibro libroBase = new LibroCoR("Libro de IT de patrones");
    Console.WriteLine(libroBase.GetDescripcion());

    BaseLibro modelo1 = new LibroCategoriaDescripcion("Libro IT", "Libro para desarrolladores");
    BaseLibro libro2 = new LibroCoR(null);
    libro2.siguiente = modelo1;
    Console.WriteLine(libro2.GetDescripcion());

    BaseLibro marca1 = new LibroDescripcion("Libro IT Tapa Dura", "TIPO");
    BaseLibro modelo2 = new LibroCategoriaDescripcion("Tecnología", null);
    modelo2.siguiente = marca1;

    BaseLibro vehiculo3 = new LibroCoR(null);
    vehiculo3.siguiente = modelo2;
    Console.WriteLine(vehiculo3.GetDescripcion());

    BaseLibro vehiculo4 = new LibroCoR(null);
    Console.WriteLine(vehiculo4.GetDescripcion());
}
~~~

Saludos y hasta la próxima.

