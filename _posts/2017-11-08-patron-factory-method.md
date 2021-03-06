---
layout: post
title: Patrón Factory Method
tags: Arquitectura
---

El objetivo del patrón **Factory** es proveer de un método abstracto de creación de un objeto delegando en las subclases concretas su creación concreta.

Lo que para los mortales como yo, esto significa que definiremos una clase base donde los métodos puedan ser sobrecargados con la implementación específica de cada clase que herede la clase base. ¿no?

Vale, más fácil todavía, tendremos unas clases con unos métodos abstractos que cuando sean heredados en cada subclase (clase hija que hereda la clase Factory) solo tendremos el nombre, las entradas y las salidas comunes a todas estas clases.

Posteriormente, en cada clase hija. Deberemos implementar estos métodos con el comportamiento de cada una de las clases.

¿Vamos con el ejemplo? ¡¡Vamos!!.

Volviendo a nuestro ejemplo de venta de libros, nos centraremos en la parte de los pedidos que pueden hacer los clientes.

La clase Cliente tiene un método que es CrearPedido, este pedido tiene dos formas de pago una en efectivo y otro de targeta.

Así, de esta premisa, nos encontramos con dos clases ClienteEfectivo y ClienteTargeta. Donde la implementación del patrón quedaría de la siguiente manera:

~~~csharp
public abstract class Pedido {
    protected double _importe;

    protected Pedido(double importe)
    {
        _importe = importe;
    }
    public abstract bool Valida();
    public abstract void Paga();
}
~~~

~~~csharp
public PedidoEfectivo : Pedido {
    public PedidoEfectivo(double importe) : base(importe) { }
    public override void Paga()
    {
        Console.WriteLine($"Método de Pago Efectivo, importe: { _importe }");
    }
    public override bool Valida() { return true; }
}
public PedidoTargeta : Pedido {
    public PedidoTargeta(double importe) : base(importe) { }
    public override void Paga()
    {
        Console.WriteLine($"Método de Pago Targeta, importe: {_importe}");
    }
    public override bool Valida() => _importe >= 0.0 && _importe <= 500.0;
}
~~~

Como vemos los métodos valida en el caso del pago en efectivo no contiene ninguna lógica de negocio, sin embargo, en el pago con tarjeta, este tiene una restricción de que el importe debe ser mayor e igual que 0 y menor e igual que 500.

~~~csharp
    private static void FactoryMethod()
    {
        PedidoTargeta pedidoEfectivo = new PedidoTargeta(100);
        if (pedidoEfectivo.Valida()) { pedidoEfectivo.Paga();}

        PedidoTargeta pedidoTargetaNoValido = new PedidoTargeta(1000);
        if (pedidoTargetaNoValido.Valida()) { pedidoTargetaNoValido.Paga(); }

        PedidoTargeta pedidoTargetaValido = new PedidoTargeta(50);
        if (pedidoTargetaValido.Valida()) { pedidoTargetaValido.Paga(); }
    }    
~~~
