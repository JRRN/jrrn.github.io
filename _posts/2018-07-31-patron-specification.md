---
layout: post
title: Patrón Specification
tags: Arquitectura
---

El patrón Specification es un patrón orientando a las aplicaciones con dominio. Es un patrón muy útil para validar queries y orientado a encapsular los objetos que pueden usarse en estas queries.

Es un patrón que separa la responsabilidad entre los objetos a recuperar y como los obtenemos.

Vamos con el ejemplo, que siempre es más claro:

~~~csharp
public interface ISpecification<TEntity>
{
    bool IsSatisfiedBy(TEntity candidate);
}

public abstract class Specification<TEntity> : ISpecification<TEntity>
{
    public abstract bool IsSatisfiedBy(TEntity candidate);
}

public class LibrosPorTemaSpecification : Specification<Book>
{
    public override bool IsSatisfiedBy(Book candidate)
    {
        return (candidate.Tema.Any(x => x.Tema));
    }
}

public Book {
    public bool ContainsLibrosPorTema { get; set;}
}

public class Main {
    public bool HayLibroDeEsteTema(string tema){
        var book = new Book{
            Tema = tema
        };

        List<Books> repositoryBooks = new bookRepository().GetAll();

        if (repositoryBooks.Any(item => item.ContainsLibrosPorTema))
        {
            return true;
        }
        return false;
    }
}
~~~

Como vemos lo que hemos hecho es encapsular el Linq que generaríamos de forma que pasando el objeto y el método, obtenemos el resultado.