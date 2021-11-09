---
layout: post
title: Patrón Bridge
tags: Arquitectura
---

El patrón **bridge** es usado para separar la implementación de un objeto, de su representación y de su interfaz. Así, conseguimos que la implementación de este objeto quede intacta, mientras que la representación puede crecer de manera independiente sin que haya un acoplamiento y tengamos que hacer cambios en el objeto con estas nuevas ampliaciones.

Tiene cierta similitud con el patrón adapter, dándole una vuelta más, donde adapter queda un poco limitado.

Para ello, a través de una clase abstracta que hereda los métodos de la clase base, sobrecargaremos estos métodos en cada clase concreta de cada tipo de libro para darle su propia implementación sin que ello afecte a los objetos MediaBook y PaperBook.

Sin más, vamos al ejemplo con el que se verá más claro su estructura y comportamiento:

~~~csharp
enum TipoLibroEnum{
    Media,
    Paper
};

public interface IBookBridge {
    void GenerarLibro(string contenido);

    TipoLibroEnum TipoDeLibro();
}

public class MediaBook : IBookBridge{
    public void GenerarLibro()
    {
        Console.WriteLine("Libro de Papel");
    }

    public TipoLibroEnum TipoDeLibro()
    {
        return TipoLibroEnum.Paper;
    }
}

public class PaperBook : IBookBridge
{
    public void GenerarLibro()
    {
        Console.WriteLine("Libro de Papel");
    }

    public TipoLibroEnum TipoDeLibro()
    {
        return TipoLibroEnum.Paper;
    }
}

public abstract class GeneradorLibro {
    public TipoLibroEnum _tipoLibroEnum;
    public IBookBridge _book;

    protected GeneradorLibro(IBookBridge book)
    {
        _book = book;
    }

    public void Genera()
    {
        _book.GenerarLibro();
    }

    public TipoLibroEnum TipoDeLibro()
    {
        return _book.TipoDeLibro();
    }

    public abstract bool ControlTipoLibro(TipoLibroEnum tipoLibro);
}

public class GeneradorLibroPapel : GeneradorLibro {
    public GeneradorLibroPapel(IBookBridge book) : base(book) { }

    public override bool ControlTipoLibro(TipoLibroEnum tipoLibro)
    {
        return tipoLibro == TipoLibroEnum.Paper;
    }
}

public class GeneradorLibroElectronico : GeneradorLibro {
    public GeneradorLibroElectronico(IBookBridge book) : base(book) { }

    public override bool ControlTipoLibro(TipoLibroEnum tipoLibro)
    {
        return tipoLibro == TipoLibroEnum.Media;
    }
}

public class Libreria{
    static void Main(string[] args){
        GeneradorLibroElectronico libroElectronico = new GeneradorLibroElectronico(new BridgePattern.MediaBook());

        Console.WriteLine(libroElectronico._tipoLibroEnum);
        if (libroElectronico.TipoDeLibro() == TipoLibroEnum.Media)
        {
            libroElectronico.Genera();
        }

        GeneradorLibroPapel libroPapel = new GeneradorLibroPapel(new BridgePattern.PaperBook());

        Console.WriteLine(libroPapel._tipoLibroEnum);
        if (libroPapel.TipoDeLibro() == TipoLibroEnum.Paper)
        {
            libroPapel.Genera();
        }
    }
}
~~~

Como hemos dicho, en nuestro caso de los libros la clase GeneradorLibro podría extenderse sin tener que tocar las clases MediaBook y PaperBook.

Saludos.

