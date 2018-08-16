---
layout: post
title: Patrón Strategy
tags: Arquitectura
---

El patrón Strategy nos permite definir varios algoritmos para aplicar sobre un objeto según nos convenga. De esta forma, podemos definir posibles acciones sobre las que decidiremos cual es la más correcta para aplicar según ciertas variables.

Aunque es un patrón bastante sencillo... Lo que realmente hace es definir algoritmos encapsulados en su clase.

Veamos el ejemplo, en este ejemplo lo que haremos es definir varias estrategias para poder calcular el IVA según el país.

~~~csharp

public interface ICalculaIVA {
    double CalculaIVA(double precio);
    void ImprimeResultado();
}

public class CalculaIVAEspaña : ICalculaIVA {
    protected double precioFinal = new double();

    public double CalculaIVA(double precio) {
        precioFinal = (precio + precio * 0.21);
        return precioFinal;
    }

    void ImprimeResultado(){
        Console.WriteLine(precioFinal);
    }
}

public class CalculaIVAMexico : ICalculaIVA {
    protected double precioFinal = new double();

    public double CalculaIVA(double precio) {
        precioFinal = (precio + precio * 0.16);
        return precioFinal;
    }

    void ImprimeResultado(){
        Console.WriteLine(precioFinal);
    }
}

public class Usuario {

    static void Main(string[] args) {
        protected ICalculaIVA _calculaIVA;

        _calculaIVA.CalculaIVA(new CalculaIVAEspaña(10));
        _calculaIVA.ImprimeResultado();

        _calculaIVA.CalculaIVA(new CalculaIVAMexico(10));
        _calculaIVA.ImprimeResultado();
    }
}

~~~

Saludos.