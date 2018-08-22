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
    protected double ImporteSinIva;
    protected double Iva;
    protected double ImporteTotal;

    public abstract void CalcularIva();

    public void CalculaPrecioTotal()
    {
        CalcularIva();
        ImporteTotal = ImporteSinIva + Iva;
    }

    public void SetImporteSinIva(double importeSinIva)
    {
        ImporteSinIva = importeSinIva;
    }

    public void Imprime()
    {
        Console.WriteLine("Pedido");
        Console.WriteLine($"Importe Sin IVA {ImporteSinIva} , IVA {Iva}");
        Console.WriteLine($"Importe Total {ImporteTotal}");
    }
}

public class PedidoEspaña : Pedido {
    public override void CalcularIva()
    {
        Iva = ImporteSinIva * 0.21;
    }
}

public class PedidoMexico : Pedido {
    public override void CalcularIva()
    {
        Iva = ImporteSinIva * 0.16;
    }
}

public class Usuario {
    static void Main(string[] args) {
        Pedido pedidoEspaña = new PedidoEspaña();
        pedidoEspaña.SetImporteSinIva(1000);
        pedidoEspaña.CalcularIva();
        pedidoEspaña.CalculaPrecioTotal();
        pedidoEspaña.Imprime();

        Pedido pedidoMexico = new PedidoMexico();
        pedidoMexico.SetImporteSinIva(1000);
        pedidoMexico.CalcularIva();
        pedidoMexico.CalculaPrecioTotal();
        pedidoMexico.Imprime();
    }
}
~~~

Saludos.
