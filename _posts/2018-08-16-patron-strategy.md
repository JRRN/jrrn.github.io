---
layout: post
title: Patrón Strategy
tags: Arquitectura
---

El patrón Strategy nos permite definir varios algoritmos para aplicar sobre un objeto según nos convenga. De esta forma, podemos definir posibles acciones sobre las que decidiremos cual es la más correcta para aplicar según ciertas variables.

Aunque es un patrón bastante sencillo... Lo que realmente hace es definir algoritmos encapsulados en su clase.

Veamos el ejemplo, en este ejemplo lo que haremos es definir varias estrategias para poder calcular el IVA según el país.

~~~csharp

public interface IBookCalculaIVA {
    double CalculaIVA(double precio);
    void ImprimeResultado();
}

public class CalculaBookIVAEspaña : IBookCalculaIVA {
    protected double precioFinal = new double();

    public double CalculaIVA(double precioBook) {
        precioFinal = (precioBook + precioBook * 0.21);
        return precioFinal;
    }

    void ImprimeResultado(){
        Console.WriteLine(precioFinal);
    }
}

public class CalculaBookIVAMexico : IBookCalculaIVA {
    protected double precioFinal = new double();

    public double CalculaIVA(double precioBook) {
        precioFinal = (precioBook + precioBook * 0.16);
        return precioFinal;
    }

    void ImprimeResultado(){
        Console.WriteLine(precioFinal);
    }
}

public class Usuario {

    static void Main(string[] args) {
        protected IBookCalculaIVA _calculaIVA;

        _calculaIVA.CalculaIVA(new CalculaBookIVAEspaña(10));
        _calculaIVA.ImprimeResultado();

        _calculaIVA.CalculaIVA(new CalculaBookIVAMexico(10));
        _calculaIVA.ImprimeResultado();
    }
}

~~~

Saludos.