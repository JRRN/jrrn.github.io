---
layout: post
title: Patrón Decorator
tags: Arquitectura
---
El patrón decorator nos permite agregar de forma dinámica funcionalidades suplementarias a un objeto sin tener que modificar la interfaz de un objeto y quedando de una forma transparente de cara al cliente.

Así, el patrón decorator es una forma más para poder crear una subclase y vitaminar un objeto sin tener que tocar la clase principal de ese mismo objeto.

En nuestro sistema de libros, podemos querer ver ciertas particularidades que tienen los libros de tecnología.

Muchos pensareís "*pero si esto me lo da la herencia*" y yo os contesto "*la herencia es demasiado potente para esta vanalidad y recordad que la herencia es un mecanismo estático*" con lo que deberiamos ir tocando en todas las hereditairas si ampliamos la interfaz o el objeto Book.

¿Lo vemos con el ejemplo? Pues vamos.

~~~csharp
public interface ICatalago {
    void VerDatosLibro();
}

public class Books : ICatalago {
    public void VerDatosLibro() {
        Console.WriteLine("Mostrando Libro");
    }
}

public abstract class Decorador : ICatalago {
    protected ICatalago _catalogo;

    public Decorador(ICatalogo catalogo){
        _catalogo = catalogo;
    }

    public virtual void VerCatalogo(){
        _catalogo.VerDatosLibro();
    }
}

public class EditorialTecnologicaDecorador : Decordor {
    public EditorialTecnologicaDecorador(ICatalago catalogo) : base(catalogo) { }

    protected void VisualizaEditorialLibrosTecnicos() {
        Console.WriteLine("Editorial libro técnico.");
    }

    public override void VerCatalogo()) {
        base.VerDatosLibro();
        VisualizaEditorialLibrosTecnicos();
    }
}

public class AutorTecnologicoDecorador : Decordor {
    public AutorTecnologicaDecorador(ICatalago catalogo) : base(catalogo) { }

    protected void VisualizaAutorLibrosTecnicos() {
        Console.WriteLine("Autor técnico.");
    }

    public override void VerCatalogo() {
        base.VerDatosLibro();
        VisualizaAutorLibrosTecnicos();
    }
}

public class VistaCatalogo {
    static void Main(string[] args) {
        Book libro = new Book();
        EditorialTecnologicaDecorador editorialTechlDecorador = new EditorialTecnologicaDecorador(libro);
        AutorTecnologicaDecorador autorTechDecorador = new AutorTecnologicaDecorador(libro);
        autorTechDecorador.VerDatosLibro();
    }
}

~~~

La salida sería:

    Mostrando Libro
    Editorial libro técnico.
    Autor técnico

Saludos.