---
layout: post
title: Patrón Adapter
tags: Arquitectura
---

El patrón **adapter** se centra en convertir la interfaz de una clase en la interfaz que necesitaran los clientes. Se trata de ofrecer con una nueva interfaz la exposición de los objetos de los clientes.

En definitiva, lo que se pretende con este patrón es generar una nueva interfaz, sobre una ya existente y no dejar expuesta la clase.

En nuestro sistema de libros, crearemos una interfaz con los métodos para generar el libro, componerlo e imprimirlo.

~~~csharp
public interface IBookAdapter
{
    string Contenido { set; }
    void Compone();
    void Imprime();
    void Enviar();
}

public class PaperBook : IBookAdapter
{

    protected string _contenido;

    public string Contenido
    {
        protected get { return _contenido; }
        set { _contenido = value; }
    }

    public void Compone()
    {
        var content = Contenido;
    }

    public void Imprime()
    {
        Console.WriteLine($"Mandando a imprimir Contenido { _contenido }");
    }

    public void Enviar()
    {
        Console.WriteLine($"Enviar al cliente");
    }
}
~~~

Sin embargo, ahora vamos a crear un libro no físico, sin embargo para este tipo de libros, el mecanismo es muy parecido pero no igual.
Con lo que aquí entra en juego el patrón Adapter:

~~~csharp
public class PdfBase
{
    protected string _contenido;

    public void PdfComponeContenido(string contenido)
    {
        _contenido = contenido;
    }

    public void PdfPrevisualizar()
    {
        Console.WriteLine($"Previsualización de Contenido: { _contenido }");
    }

    public void PdfAlmacena()
    {
        Console.WriteLine($"Guardando Book");
    }

    public void PdfImprimePorPantalla()
    {
        Console.WriteLine($"Imprime por pantalla { _contenido }");
    }

    public void PdfEnviar()
    {
        Console.WriteLine($"Enviando link de descarga al cliente");
    }
}
~~~

Como podemos ver la clase PdfBase es independiente a la jerarquía que hasta ahora tenemos. Sin embargo, podemos ver métodos que podrían pertenecer a la interfaz IBook, así que nos toca "adaptar" esta lógica para que acepte la jerarquía:

~~~csharp
public class PdfBook : IBookAdapter
{
    protected PdfBase _pdfBase = new PdfBase();

    public string Contenido
    {
        set => _pdfBase.PdfComponeContenido(value);
    }

    public void Compone()
    {
        _pdfBase.PdfPrevisualizar();
        _pdfBase.PdfAlmacena();
    }

    public void Imprime()
    {
        _pdfBase.PdfImprimePorPantalla();
    }

    public void Enviar()
    {
        _pdfBase.PdfEnviar();
    }
}
~~~

Como podemos ver, la clase PdfBook ha implementado la interfaz IBook y de esta forma hemos no hemos tenido que dejar expuesto los métodos concretos de la clase PdfBase, que son desconocidos para el cliente.

Finalmente, para generar una salida tendremos:

~~~csharp
public class Servicio {
    static void Main(string[] args){
        IBookAdapter paperBook = new PaperBook { Contenido = "Soy un libro físico"};
        paperBook.Compone();
        paperBook.Imprime();
        paperBook.Enviar();

        IBookAdapter mediaBook = new PdfBook {Contenido = "Soy un libro digital"};
        mediaBook.Compone();
        mediaBook.Imprime();
        mediaBook.Enviar();
    }
}
~~~

Un saludo.

