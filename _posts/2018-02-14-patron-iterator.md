---
layout: post
title: Patrón Iterator
tags: Arquitectura
---
El patrón **iterator** nos proporciona un mecanismo para recorrer colecciones de objetos de forma secuencial sin tener conocimiento de cómo están implementadas estas colecciones.

Vamos con el ejemplo:

~~~csharp
public abstract class Item
{
    protected string _descripcion;

    protected Item(string descripcion)
    {
        _descripcion = descripcion;
    }

    public bool PalabraClaveValida(string palabraClave)
    {
        return _descripcion.Contains(palabraClave);
    }
}

public class BookIterator : Item
{
    public BookIterator(string descripcion) : base(descripcion) { }

    public void Visualiza()
    {
        Console.WriteLine($"Descripción del Libro: { _descripcion}");
    }
}

public abstract class Iterador<TItem> where TItem : Item
{
    public string palabraClaveConsulta { protected get; set; }
    protected int indice;
    public IList<TItem> contenido { protected get; set; }

    public void Inicio()
    {
        indice = 0;
        int length = contenido.Count;
        while (indice < length && !contenido[indice].PalabraClaveValida(palabraClaveConsulta)) {
            indice++;
        }
    }

    public void Siguiente()
    {
        int length = contenido.Count;
        indice++;
        while (indice < length && !contenido[indice].PalabraClaveValida(palabraClaveConsulta)) {
            indice++;
        }
    }

    public TItem item()
    {
        return indice < contenido.Count ? contenido[indice] : null;
    }
}

public class IteradorBook : Iterador<BookIterator> { }

public abstract class Catalogo<TElemento, TIterador>
    where TElemento : Item
    where TIterador : Iterador<TElemento>, new()
{
    protected IList<TElemento> contenido = new List<TElemento>();

    public TIterador Busqueda(string palabraClaveConsulta)
    {
        TIterador resultado = new TIterador
        {
            contenido = contenido,
            palabraClaveConsulta = palabraClaveConsulta
        };

        return resultado;
    }
}

public class CatalogoBook : Catalogo<BookIterator, IteradorBook>
{
    public CatalogoBook()
    {
        contenido.Add(new BookIterator("Libro PDF"));
        contenido.Add(new BookIterator("Gran libro en PDF"));
        contenido.Add(new BookIterator("Libro de gran calidad"));
    }
}

public class Usuario {
    static void Main(string[] args) {
        CatalogoBook catalogo = new CatalogoBook();
        IteradorBook iterador = catalogo.Busqueda("PDF");
        BookIterator libro;
        iterador.Inicio();
        libro = iterador.item();
        while (libro != null)
        {
            libro.Visualiza();
            iterador.Siguiente();
            libro = iterador.item();
        }
    }
}
~~~

Descripción del Libro: Libro PDF
Descripción del Libro: Gran libro en PDF

Hasta la próxima.
