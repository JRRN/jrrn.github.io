---
layout: post
title: Patrón Chain of Responsability
tags: Arquitectura
---
El patrón Chain Of Responsability nos ayuda a crear una secuencia de unión entre objetos tal que si el objeto más interno de la cadena no es capaz de dar una respuesta, uno de los objetos de nivel superior será el encargado de darla. Esta respuesta será a nivel del contexto en que el objeto se encuentre y sea capaz de responder.

Como siempre, mejor con un ejemplo, ¿no?

Os acordáis de nuestro ejemplo de venta de libros...

En él, tenemos libros, dentro de libros tenenemos categoría de libros y dentro de la categoría de libros tenemos el libro en cuestión.

Empezamos:
~~~csharp
public abstract class BaseLibro {
    public BaseLibro siguiente {protected get; set;}

    private string descripcionBase() {
        return "Descripción base: Es un libro."
    }

    protected abstract string descripcion {get;}

    public string GetDescripcion() {
        string result;
        result = descripcion;

        if(result != null) {
            return result;
        }
        if(siguiente != null) {
            return siguiente.GetDescripcion();
        }
        return descripcionBase();
    }
}

public class Libro : BaseLibro {
    protected string _libroDescripcion;

    public Libro(string descripcion) {
        _libroDescripcion = descripcion;
    }

    protected override string descripcion {
        get { return _libroDescripcion; }
    }
}

public class LibroCategoriaDescripcion : BaseLibro {
    protected string _categoriaDescripcion;
    protected string _categoria;

    public Libro(string descripcion, string categoria) {
        _categoriaDescripcion = descripcion;
        _categoria = categoria;
    }

    protected override string descripcion {
        get
        {
            if(_categoriaDescripcion != null) {
                return $"{La categoria {_categoria} : _categoriaDescripcion}";
            } else {
                return null;
            }
        }
    }
}

public class LibroDescripcion : BaseLibro {
    protected string _libroDescripcion;
    protected string _libro;

    public Libro(string descripcion, string libro) {
        _libroDescripcion = descripcion;
        _libro = libro;
    }

    protected override string descripcion {
        get
        {
            if(_libroDescripcion != null) {
                return $"{El libro {_libro} : _libroDescripcion}";
            } else {
                return null;
            }
        }
    }
}
~~~

Saludos y hasta la próxima.