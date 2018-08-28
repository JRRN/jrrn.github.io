---
layout: post
title: Patrón Memento
tags: Arquitectura
---

El patrón memento previene en la encapsulación de un objeto el estado en que se encuentra en cada momento. De esta forma, si por algún motivo, necesitamos hacer un rollback de estos cambios del objeto, podamos restaurar sin romper nada.

Es como tener un pila de estados de como ha ido cambiando el objeto y si es necesario, poder volver a un punto determinado.

Vamos con la implementación.

~~~csharp
public interface Memento { }

public class MementoImplementation : Memento {
    protected IList<OpcionBook> _bookOptions = new List<OpcionBook>();

    public IList<OpcionBook> State
    {
        get => _bookOptions;
        set
        {
            _bookOptions.Clear();
            foreach (OpcionBook bookOption in value)
            {
                _bookOptions.Add(bookOption);
            }
        }
    }
}

public class CompraOpciones {
    protected IList<OpcionBook> bookOptions = new List<OpcionBook>();

    public IMemento AgregaOpciones(OpcionBook bookOption)
    {
        MementoImplementation result = new MementoImplementation();
        result.State = bookOptions;

        IList<OpcionBook> bookOptionsNotSupported = bookOption.BookOptionsNotSupported;

        foreach (OpcionBook bOption in bookOptionsNotSupported)
        {
            bookOptions.Remove(bOption);
        }

        bookOptions.Add(bookOption);

        return result;
    }

    public void Anula(IMemento memento)
    {
        if (!(memento is MementoImplementation mementoImplementation))
        {
            return;
        }

        bookOptions = mementoImplementation.State;
    }

    public void Visualiza()
    {
        Console.WriteLine("Estados:");

        foreach (OpcionBook bookOption in bookOptions)
        {
            bookOption.Ver();
        }
    }
}

public class OpcionBook {
    protected string _nombre;
    public IList<OpcionBook> BookOptionsNotSupported { get; protected set; }

    public OpcionBook(string nombre)
    {
        BookOptionsNotSupported = new List<OpcionBook>();
        _nombre = nombre;
    }

    public void AgregaOpcionIncompatible(OpcionBook bookOptionIncompatible)
    {
        if (!BookOptionsNotSupported.Contains(bookOptionIncompatible))
        {
            BookOptionsNotSupported.Add(bookOptionIncompatible);
            bookOptionIncompatible.AgregaOpcionIncompatible(this);
        }
    }

    public void Ver() => Console.WriteLine($"opcion : {_nombre}");
}

public void Main() {
    IMemento memento;

    OpcionBook op1 = new OpcionBook("Tapa dura");
    OpcionBook op2 = new OpcionBook("Tapa Blanda");
    OpcionBook op3 = new OpcionBook("Tapa Encuadernado");

    op1.AgregaOpcionIncompatible(op3);
    op2.AgregaOpcionIncompatible(op3);

    CompraOpciones compraOpciones = new CompraOpciones();
    compraOpciones.AgregaOpciones(op1);
    compraOpciones.AgregaOpciones(op2);
    compraOpciones.Visualiza();

    memento = compraOpciones.AgregaOpciones(op3);
    compraOpciones.Visualiza();
    compraOpciones.Anula(memento);
    compraOpciones.Visualiza();
}
~~~

Saludos.
