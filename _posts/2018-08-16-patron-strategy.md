---
layout: post
title: Patrón Strategy
tags: Arquitectura
---

El patrón Strategy nos permite definir varios algoritmos para aplicar sobre un objeto según nos convenga. De esta forma, podemos definir posibles acciones sobre las que decidiremos cual es la más correcta para aplicar según ciertas variables.

Aunque es un patrón bastante sencillo... Lo que realmente hace es definir algoritmos encapsulados en su clase.

Veamos el ejemplo, en este ejemplo lo que haremos es definir varias estrategias para poder calcular el IVA según el país.

~~~csharp

public interface IBookCalculaIva {
    double CalculaIva(double precio);
    void ImprimeResultado();
}

public class CalculaBookIvaEspaña : IBookCalculaIva
{
    protected double PrecioFinal;

    public double CalculaIva(double precioBook)
    {
        PrecioFinal = precioBook + precioBook * 0.21;
        return PrecioFinal;
    }

    public void ImprimeResultado()
    {
        Console.WriteLine(PrecioFinal);
    }
}

public class CalculaBookIvaMexico : IBookCalculaIva
{
    protected double PrecioFinal;

    public double CalculaIva(double precioBook)
    {
        PrecioFinal = precioBook + precioBook * 0.16;
        return PrecioFinal;
    }

    public void ImprimeResultado()
    {
        Console.WriteLine(PrecioFinal);
    }
}

public class Usuario {

    static void Main(string[] args) {
        protected IBookCalculaIVA _calculaIVA;

        _calculaIva.CalculaIva(new CalculaBookIvaEspaña().CalculaIva(10));
        _calculaIva.ImprimeResultado();

        _calculaIva.CalculaIva(new CalculaBookIvaMexico().CalculaIva(10));
        _calculaIva.ImprimeResultado();
    }
}

~~~

Saludos.
