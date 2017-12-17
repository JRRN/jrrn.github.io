---
layout: post
title: Patrón Bridge
tags: Arquitectura
---

El patrón bridge es usado para separar la implementación de un objeto, de su representación y de su interfaz. Así, conseguimos que la implementación de este objeto quede intacta, mientras que la representación puede crecer de manera independiente sin que haya un acomplamiento y tengamos que hacer cambios en el objeto con estas nuevas ampliaciones.

Tiene cierta similitud con el patrón adapter, dándole una vuelta más, donde adapter queda un poco limitado.

Para ello, a través de una clase abstracta que hereda los métodos de la clase base, sobrecargaremos estos métodos en cada clase concreta de cada tipo de libro para darle su propia implentación sin que ello afecte a los objetos MediaBook y PaperBook.

Sin más, vamos al ejemplo con el que se verá más claro su estrucutura y comportamiento:

~~~csharp
enum TipoLibroEnum{
    Media,
    Paper
};

public interface IBook {
    void GenerarLibro(string contenido);

    TipoLibroEnum TipoDeLibro();
}

public class MediaBook : IBook{
    public void GenerarLibro(string contenido){
        Console.WriteLine("Libro Electronico" );
    }

    public TipoLibroEnum TipoDeLibro(){
        return TipoLibroEnum.Media;
    }
}

public class PaperBook : IBook{
    public void GenerarLibro(string contenido){
        Console.WriteLine("Libro Papel" );
    }

    public TipoLibroEnum TipoDeLibro(){
        return TipoLibroEnum.Paper;
    }
}

public abstract class GeneradorLibro {
    protected TipoLibroEnum _tipoLibroEnum;
    protected IBook _book;

    public GeneradorLibro(IBook book){
        _book = book;
    }

    public void Genera() {
        _book.GenerarLibro(contenido);
    }

    public TipoLibroEnum TipoDeLibro() {
        return _book.TipoDeLibro();
    }

    protected abstract bool controlTipoLibro(TipoLibroEnum tipoLibro);
}

public class GeneradorLibroPapel : GeneradorLibro {
    public GeneradorLibroPapel(GeneradorLibro) : base(book){}

    protected override TipoLibroEnum controlTipoLibro(TipoLibroEnum tipoLibro){
        return TipoLibroEnum.Paper;
    }
}

public class GeneradorLibroElectronico : GeneradorLibro {
    public GeneradorLibroElectronico(GeneradorLibro) : base(book){}

    protected override TipoLibroEnum controlTipoLibro(TipoLibroEnum tipoLibro){
        return TipoLibroEnum.Media;
    }
}

public class Libreria{
    static void Main(string[] args){
        GeneradorLibroPapel libroElectronico = new GeneradorLibroPapel(new MediaBook());

        Console.WriteLine(libroElectronico.controlTipoLibro().Tostring())
        if(libroElectronico.controlTipoLibro == TipoLibroEnum.Media){
            libroElectronico.GenerarLibro()
        }

        GeneradorLibroPapel libroPapel = new GeneradorLibroElectronico(new PaperBook());

        Console.WriteLine(libroPapel.controlTipoLibro().Tostring())
        if(libroPapel.controlTipoLibro == TipoLibroEnum.Papel){
            libroPapel.GenerarLibro()
        }
    }
}
~~~

Como hemos dicho, en nuestro caso de los libros la clase GeneradorLibro podría extenderse sin tener que tocar las clases  MediaBook y PaperBook.

Saludos.