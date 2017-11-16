---
layout: post
title: Patrón Adapter
tags: Arquitectura
---

El patrón adapter se centra en convertir la interfaz de una clase en la interfaz que necesitaran los clientes. Se trata de ofrecer con una nueva interfaz la exposición de los objetos de los clientes.

En definitiva, lo que se prentende con este patrón es generar una nueva interfaz, sobre una ya existente y no dejar expuesta la clase.

En nuestro sistema de libros, crearemos una interfaz con los métodos para generar el libro, componerlo e imprimirlo.

~~~csharp
public interface IBook {
    string contenido {set;}
    void Compone();
    void Imprime();
    void Enviar();
}

public class PaperBook : IBook {
    protected string _contenido

    public string contenido {
        protected get { return _contenido; }
        set { _contenido = value }
    }

    public void Compone() {
        var contenido = ComponerContenido(contenido);
    }

    public void Imprime() {
        Consolte.WriteLine($"Mandando a imprimir Contenido {contenido}");
    }

    public void Enviar(){
        Consolte.WriteLine($"Enviar al cliente");
    }
}
~~~

Sin embargo, ahora vamos a crear un libro no físico, sin emabrgo para este tipo de libros, el mecanismos es muy parecido pero no igual.
Con lo que aquí entra en juego el patrón Adapter:

~~~csharp
public class PdfBase {
    protected string _contenido;

    public void PdfComponeContenido(string contenido) {
        _contenido = contenido;
    }

    public void PdfPrevisualizar() {
        Consolte.WriteLine($"Previsualización de Contenido: { _contenido }");
    }

    public void PdfAlmacena() {
        Consolte.WriteLine($"Guardando de Book");
    }

    public void PdfImprimePorPantalla() {
        Consolte.WriteLine($"Imprime por pantall { _contenido }");
    }

    public void PdfEnviar(){
        Consolte.WriteLine($"Enviando link de descarga al cliente");
    }
}
~~~

Como podemos ver la clase PdfBase es independiente a la jerarquía que hasta ahora tenemos. Sin embargo podemos ver métodos que podrian pertenecer a la interfaz IBook, así que nos toca "adaptar" esta lógica para que acepte la jerarquía:

~~~csharp
public class PdfBook : IBook {
    protected PdfBase _pdfBase = new PdfBase();

    public string contenido {
        set { _pdfbase.PdfComponeContenido(value); }
    }

    public void Compone(){
        _pdfBase.PdfPrevisualizar();
        _pdfBase.PdfAlmacena();
    }

    public void Imprime(){
        _pdfBase.PdfImprimePorPantalla();
    }

    public void Enviar(){
        _pdfBase.PdfEnviar();
    }
}
~~~

Como podemos ver, la clase PdfBook ha implementado la interfaz IBook y de esta forma hemos no hemos tenido que dejar expuesto los métodos concretos de la clase PdfBase, que son desconocidos para el cliente.

Finalmente, para generar una salida tendremos:

~~~csharp
public class Servicio{
    static void Main(string[] args){
        Ibook paperBook, mediaBook;

        paperBook = new PaperBook();
        paperbook.contenido = "Soy un libro físico";
        paperbook.Componer();
        paperbook.Imprime();
        paperbook.Enviar();

        mediaBook = new PdfBook();
        mediaBook.contenido = "Soy un libro digital";
        mediaBook.Componer();
        mediaBook.Imprime();
        mediaBook.Enviar();
    }
}
~~~

un saludo.