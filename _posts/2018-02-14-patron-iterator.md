---
layout: post
title: Patrón Iterator
tags: Arquitectura
---
El patrón **iterator** nos proporciona un mecanismo para recorrer colecciones de objetos de forma secuencial sin tener conocimiento de cómo están implementadas estas colecciones.

Vamos con el ejemplo:

~~~csharp
public abstract class Item {
    protected string _descripcion;

    public Item(string descripcion) {
        _descripcion = descripcion;
    }

    public bool palabraClaveValida(string palabraClave) {
        return descripcion.Contains(palabraClave);
    }
}

public class Book : Item {
    public Book(string descripcion) : base(descripcion) { }

    public void visualiza() {
        Console.WriteLine($"Descripción del Libro: {descripcion}");
    }
}

public abstract class Iterador<TItem>  where TItem : Item {
    public string palabraClaveConsulta { protected get; set; }
    protected int indice;
    public IList<TElemento> contenido { protected get; set; }

    public void inicio() {
        indice = 0;
        int length = contenido.Count;
        while ((indice < length) && (!contenido[indice]palabraClaveValida(palabraClaveConsulta))) {
            indice++;
        }
    }

    public void siguiente() {
        int length = contenido.Count;
        indice++;
        while ((indice < length) && (!contenido[indice]palabraClaveValida(palabraClaveConsulta))) {
            indice++;
        }
    }

    public TElemento item() {
        if (indice < contenido.Count){
            return contenido[indice];
        }
        else {
            return null;
        }
    }
}

public class IteradorBook : Iterador<Book> {}

public abstract class Catalogo<TElemento, TIterador>
    where TElemento : Elemento
    where TIterador : Iterador<TElemento>, new()
{
    protected IList<TElemento> contenido = new List<TElemento>();

    public TIterador busqueda(string palabraClaveConsulta) {
        TIterador resultado = new TIterador();
        resultado.contenido = contenido;
        resultado.palabraClaveConsulta = palabraClaveConsulta;
        return resultado;
    }
}

public class CatalogoBook : Catalogo<Book, IteradorBook> {
    public CatalogoBook() {
       contenido.Add(new Book("Libro PDF"));
       contenido.Add(new Book("Gran libro en PDF"));
       contenido.Add(new Book("Libro de gran calidad"));
    }
}

public class Usuario {
    static void Main(string[] args) {
        CatalogoBook catalogo = new CatalogoBook();
        IteradorBook iterador = catalogo.busqueda("PDF");
        Book libro;
        iterador.inicio();
        libro = iterador.item();
        while (libro != null) {
            libro.visualiza();
            iterador.siguiente();
            libro = iterador.item();
        }
    }
}

Descripción del Libro: Libro PDF
Descripción del Libro: Gran libro en PDF
~~~

Hasta la próxima.