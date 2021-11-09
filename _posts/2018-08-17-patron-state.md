---
layout: post
title: Patrón State
tags: Arquitectura
---

El patrón State nos ayuda a que un objeto se comporte de forma diferente según un flag de estado. De esta forma, según cual sea el flag de estado, el objeto se comportará de una forma o de otra.

El ejemplo más simple para entender este patrón, es en los pedidos, si el pedido ha pasado por todos los estados y ha llegado al estado "Pedido Entregado", no tiene sentido que podamos ejecutar un método que lo que haga es cambiar la dirección de entrega, a pesar de que internamente, este objeto(pedido) tenga ese método y que sin embargo, solo se pueda ejecutar mientras el objeto está en "Preparando el envío".

Vayamos con el ejemplo:

~~~csharp
public class PedidoState {
    protected IList<ProductoState> productos = new List<ProductoState>();

    public IList<ProductoState> Productos => productos;

    protected EstadoPedido EstadoPedido;

    public PedidoState() {
        EstadoPedido = new PedidoEnCurso(this);
    }

    public void AgregaProducto(ProductoState producto)
    {
        EstadoPedido.AgregaProducto(producto);
    }

    public void QuitaProducto(ProductoState producto)
    {
        EstadoPedido.QuitaProducto(producto);
    }

    public void QuitaTodo()
    {
        EstadoPedido.QuitaTodo();
    }

    public void EstadoSiguiente()
    {
        EstadoPedido = EstadoPedido.EstadoSiguiente();
    }

    public void Imprime()
    {
        Console.WriteLine("Contenido del pedido:");
        foreach (var producto in Productos)
        {
            producto.Imprime();
        }

        Console.WriteLine();
    }
}

public abstract class EstadoPedido {
        protected PedidoState Pedido;

        protected EstadoPedido(PedidoState pedido) {
            Pedido = pedido;
        }

        public abstract void AgregaProducto(ProductoState producto);
        public abstract void QuitaTodo();
        public abstract void QuitaProducto(ProductoState producto);
        public abstract EstadoPedido EstadoSiguiente();
}

public class PedidoEnCurso : EstadoPedido {
    public PedidoEnCurso(PedidoState pedido) : base(pedido) { }

    public override void AgregaProducto(ProductoState producto)
    {
        Pedido.Productos.Add(producto);
    }

    public override void QuitaTodo()
    {
        Pedido.Productos.Clear();
    }

    public override void QuitaProducto(ProductoState producto)
    {
        Pedido.Productos.Remove(producto);
    }

    public override EstadoPedido EstadoSiguiente()
    {
        return new PedidoConfirmado(Pedido);
    }
}

public class PedidoConfirmado : EstadoPedido {
    public PedidoConfirmado(PedidoState pedido) : base(pedido) { }

    public override void AgregaProducto(ProductoState producto)
    {
    }

    public override void QuitaTodo()
    {
        Pedido.Productos.Clear();
    }

    public override void QuitaProducto(ProductoState producto)
    {
    }

    public override EstadoPedido EstadoSiguiente()
    {
        return new PedidoEntregado(Pedido);
    }
}

public class PedidoEntregado : EstadoPedido {
    public PedidoEntregado(PedidoState pedido) : base(pedido) { }

    public override void AgregaProducto(ProductoState producto) { }

    public override void QuitaTodo() { }

    public override void QuitaProducto(ProductoState producto) { }

    public override EstadoPedido EstadoSiguiente()
    {
        return this;
    }
}

public class Producto {
    public class ProductoState
    {
        protected string Nombre;

        public ProductoState(string nombre)
        {
            Nombre = nombre;
        }

        public void Imprime()
        {
            Console.WriteLine($"Producto: {Nombre}");
        }
    }
}

public class Usuario {
    static void Main(string[] args) {
        PedidoState pedido = new PedidoState();
        pedido.AgregaProducto(new ProductoState("Book 1"));
        pedido.AgregaProducto(new ProductoState("Book 2"));
        pedido.Imprime();
        pedido.EstadoSiguiente();
        pedido.AgregaProducto(new ProductoState("Book 3"));
        pedido.QuitaTodo();
        pedido.Imprime();

        PedidoState pedido2 = new PedidoState();
        pedido2.AgregaProducto(new ProductoState("Book 10"));
        pedido2.AgregaProducto(new ProductoState("Book 20"));
        pedido2.Imprime();
        pedido2.EstadoSiguiente();
        pedido2.Imprime();
        pedido2.EstadoSiguiente();
        pedido2.QuitaTodo(); //En este estado no hará nada
        pedido2.Imprime();
    }
}
~~~
