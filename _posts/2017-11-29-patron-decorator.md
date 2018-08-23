---
layout: post
title: Patrón Decorator
tags: Arquitectura
---

El patrón **decorator** nos permite agregar de forma dinámica funcionalidades suplementarias a un objeto sin tener que modificar la interfaz de un objeto y quedando de una forma transparente de cara al cliente.

Así, el patrón decorator es una forma más para poder crear una subclase y vitaminar un objeto sin tener que tocar la clase principal de ese mismo objeto.

En nuestro sistema de libros, podemos querer ver ciertas particularidades que tienen los libros de tecnología.

Muchos pensaréis "*pero si esto me lo da la herencia*" y yo os contesto "*la herencia es demasiado potente para esta banalidad y recordad que la herencia es un mecanismo estático*" con lo que deberíamos ir tocando en todas las hereditarias si ampliamos la interfaz o el objeto Book.

¿Lo vemos con el ejemplo? Pues vamos.

~~~csharp
public interface ICatalogo
{
    void VerDatosLibro();
}

public class Books : ICatalogo
{
    public void VerDatosLibro()
    {
        Console.WriteLine("Mostrando Libro");
    }
}

public abstract class Decorador : ICatalogo
{
    protected ICatalogo _catalogo;

    protected Decorador(ICatalogo catalogo)
    {
        _catalogo = catalogo;
    }

    public virtual void VerCatalogo()
    {
        VerDatosLibro();
    }

    public void VerDatosLibro()
    {
        _catalogo.VerDatosLibro();
    }
}

public class EditorialTecnologicaDecorador : Decorador
{
    public EditorialTecnologicaDecorador(ICatalogo catalogo) : base(catalogo) { }

    protected void VisualizaEditorialLibrosTecnicos()
    {
        Console.WriteLine("Editorial libro técnico.");
    }

    public override void VerCatalogo()
    {
        base.VerDatosLibro();
        VisualizaEditorialLibrosTecnicos();
    }
}

public class AutorTecnologicoDecorador : Decorador
{
    public AutorTecnologicoDecorador(ICatalogo catalogo) : base(catalogo) { }

    protected void VisualizaAutorLibrosTecnicos()
    {
        Console.WriteLine("Autor técnico.");
    }

    public override void VerCatalogo()
    {
        base.VerDatosLibro();
        VisualizaAutorLibrosTecnicos();
    }
}

public class VistaCatalogo {
    static void Main(string[] args) {
        DecoratorPattern.Books libro = new DecoratorPattern.Books();
        EditorialTecnologicaDecorador editorialTechlDecorador = new EditorialTecnologicaDecorador(libro);
        AutorTecnologicoDecorador autorTechDecorador = new AutorTecnologicoDecorador(libro);
        autorTechDecorador.VerCatalogo();
        editorialTechlDecorador.VerCatalogo();
    }
}

~~~

La salida sería:

    Mostrando Libro
    Editorial libro técnico.
    Autor técnico

Saludos.

