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
    protected IList<BookOptions> bookOptions = new List<BookOptions>();

    public IList<BookOptions> State
    {
        get { return bookOptions};
        set {
            bookOptions.Clear();
            foreach (bookOptions bookOption in value) bookOptions.Add(bookOption);
        }
    }
}

public class CompraOpciones {
    protected IList<BookOptions> bookOptions = new List<BookOptions>();

    public Memento AgregaOpciones(BookOptions bookOption){
        MementoImplementation result = new MementoImplementation();
        result.State = bookOption;

        IList<BookOptions> bookOptionsNotSupported = bookOption.bookOptionNotSupported;

        foreach(BookOptions bookOption in bookOptionsNotSupported) {
            bookOptions.Remove(bookOption);
        }

        bookOptions.Add(bookOptions);

        return result;
    }

    public void Anula(Memento memento) {
        MementoImplementation mementoImplementation = memento as MementoImplementation;
        if(MementoImplementation == null) return
        bookOptions = MementoImplementation.State;
    }

    public void Visualiza() {
        Console.Writeline("Estados");

        foreach (bookOptions bookOption in bookOptions) {
            bookOption.Visualiza();
        }
    }
}

public class OpcionBook {
    protected string _nombre;
    IList<BookOptions> bookOptionsNotSupported { get; protected set; }

    public OpcionBook(string nombre){
        bookOptionsNotSupported = new List<BookOptions>();
        _nombre = nombre;
    }

    public void agregaOpcionIncompatible(BookOption bookOptionIncompatible) {
        if(!bookOptionsNotSupported.Contains(bookOptionIncompatible)){
            bookOptionsNotSupported.Add(bookOptionIncompatible);
            bookOptionIncompatible.agregaOpcionIncompatible(this);
        }
    }

    public void Ver() {
        Console.WriteLine($"opcion : {nombre}")
    }
}

public void Main() {
    Memento memento;

    OpcionBook op1 = new  OpcionBook("Tapa dura");
    OpcionBook op2 = new  OpcionBook("Tapa Blanda");  
    OpcionBook op3 = new  OpcionBook("Tapa Encuadernado");

    op1.agregaOpcionIncompatible(op3);
    op2.agregaOpcionIncompatible(op3);

    CompraOpciones compraOpciones = new CompraOpciones();
    compraOpciones.AgregaOpciones(op1);
    compraOpciones.AgregaOpciones(op2);
    compraOpciones.Visualiza();

    compraOpciones.Anula(memento);
    compraOpciones.Visualiza();
}
~~~