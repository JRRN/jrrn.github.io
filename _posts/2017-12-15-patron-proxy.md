---
layout: post
title: Patrón Proxy
tags: Arquitectura
---

El patrón **proxy** se utiliza para diseñar un objeto que sustituye a otro objeto que controla su acceso. El objeto proxy es el que queda expuesto en la capa de servicios o presentación siendo idéntico y con mismo contrato que el original.

El claro ejemplo, son las entidades que solemos recoger de la capa de acceso a datos y que mapeamos contra la capa de negocio, dominio, etc...

Para nuestro ejemplo de los libros, tenemos una página web con un listado de libros y que haciendo clic sobre cada título podemos ver una descripción más completa del libro seleccionado. En este caso, podríamos tener cargadas todas estas descripciones desde la primera carga, pero mejor, si las recuperamos cuando son solicitadas y las que son solicitadas.

~~~csharp

public interface IBook {
    void Renderiza();
    void CargaDescripcion();
}

public class DescripcionProxy : IBook {
    protected Datos book = null;
    protected string descripcion = "Desccripción Simple";

    public void CargaDescripcion()
    {
        if (book == null)
        {
            book = new Datos();
            book.CargaDescripcion();
        }
        else { book.CargaDescripcion(); }

    }

    public void Renderiza()
    {
        if (book != null)
        {
            book.Renderiza();
        }
        else
        {
            Renderiza(descripcion);
        }
    }

    public void Renderiza(string descripcion) => Console.WriteLine($"{descripcion}");
}

public class VistaBook
{
    static void Main(string[] args) {
        IBook book = new DescripcionProxy();

        book.Renderiza();
        book.CargaDescripcion();
    }
}
~~~

Así obtendríamos esta salida:

Mostrar descripción
Carga descripción
Mostrando descripción
Muestra Descripción

Saludos.

