---
layout: post
title: Patrón Observer
tags: Arquitectura
---

El patrón Observer se usa para crear una dependencia entre el objeto y otros que estén anexados a él. De esta forma, cuando se realiza una modificación en el primer objeto, los objetos anexados a el, reciben esta actualización.

Aunque es clara la definición, lo que se trata es de que si realizamos un cambio de, por ejemplo una propiedad  "nombre", en el objeto principal, los demás se enteran de que esa propiedad nombre ha cambiado de forma automática.

Vamos con el ejemplo:

~~~csharp
public abstract class ObjetoPrincipal {
    protected IList<Observer> observadores = new List<Observer>();

    public void Agrega(Observer observador) {
        observadores.Add(observador);
    }

    public void Quita(Observer observadir) {
        observadores.Remove(observador);
    }

    public void Actualiza() {
        foreach (var observador in observadores) {
            observador.Actualiza();
        }
    }
}

public interface Observer {
    void Actualiza();
}

public class Book : ObjetivoPrincipal {
    protected string _descripcion;
    protected string _precio;

    public string Descripcion {
        get { return _descripcion; }
        set { _descripcion = value; this.Actualiza(); }
    }

    public string Precio {
        get { return _descripcion; }
        set { _descripcion = value; this.Actualiza(); }
    }
}

public class BookView : Observer {
    protected Book book;
    protected string texto = String.Empty;

    public BookView(Book book) {
        this.book = book;
        book.Agrega(this);
        ActualizaTexto();
    }

    protected void ActualizaTexto() {
        texto = $"Descripción {book.Descripcion}, precio {book.Precio}";
    }

    public void Actualiza() {
        ActualizaTexto();
        this.Imprime();
    }

    public void Imprime() {
        Console.WriteLine (texto);
    }
}

public class Usuario {
    static void Main(string[] args) {
        Book book = new Book();
        book.Descripcion = "Libro de IT";
        book.Precio = "10";

        BookView bookView = new BookView(book);
        bookView.Imprime();

        book.Descripcion = "Libro de IT Barato";

        BookView bookView2 = new BookView(book);
        book.Descripcion = "Libro de IT Muy Barato";
    }
}
~~~

Como se puede ver si ejecutamos el código, es que cada cambio de Descripcion desencadena una actualización en todos los objetos BookView.

Saludos.