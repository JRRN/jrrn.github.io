---
layout: post
title: Patrón Template Method
tags: Arquitectura
---

El patrón Template Method nos permite definir un esqueleto de métodos abstractos en los que cada clase concreta sobrecargará estos métodos para definir su comportamiento específico y cuya implementación difiera en algunos pasos.

De esta forma, definimos una clase con métodos abstractos como si fuera un contrato o interfaz, y posteriomente definiremos una clase que herede esta superclase y en la que codificaremos cada método con su algoritmo específico.

Una vez más usaremos el ejemplo de los libros y le daremos otra solución al calculo del IVA desde la perspectiva Template Method.

Veamos el ejemplo:

~~~csharp

public abstract class Pedido {
    protected double importeSinIVA;
    protected double IVA;
    protected double importeTotal;

    protected abstract void CalcularIVA();

    public void CalculaPrecioTotal() {
        this.CalcularIVA();
        importeTotal = importeSinIVA + IVA;
    }

    public void setImporteSinIVA(double importeSinIVA) {
        this.importeSinIVA = importeSinIVA;
    }

    public void Imprime() {
        Console.WriteLine("Pedido");
        Console.WriteLine($"Importe Sin IVA {importeSinIVA} , IVA {IVA}");
        Console.WriteLine($"Importe Total {importeTotal}");
    }
}

public class PedidoEspaña : Pedido {
    protected override void CalcularIVA(){
        IVA = importeSinIVA * 0.21;
    }
}

public class PedidoMexico : Pedido {
    protected override void CalcularIVA(){
        IVA = importeSinIVA * 0.16;
    }
}

public class Usuario {
    static void Main(string[] args) {
        Pedido pedidoEspaña = new PedidoEspaña();
        pedidoEspaña.setImporteSinIVA(1000);
        pedidoEspaña.CalcularIVA();
        pedidoEspaña.Imprime();

        Pedido pedidoMexico = new PedidoMexico();
        pedidoMexico.setImporteSinIVA(1000);
        pedidoMexico.CalcularIVA();
        pedidoMexico.Imprime();
    }
}
~~~

Saludos.