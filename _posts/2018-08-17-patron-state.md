---
layout: post
title: Patrón State
tags: Arquitectura
---

El patrón State nos ayuda a que un objeto se comporte de forma diferente según un flag de estado. De esta forma, según cual sea el flag de estado, el objeto se comportará de una forma o de otra.

El ejemplo más simple para entender este patrón, es en los pedidos, si el pedido ha pasado por todos los estados y ha llegado al estado "Pedido Entregado", no tiene sentido que podamos ejecutar un método que lo que haga es cambiar la dirección de entrega, a pesar de que internamente, este objeto(pedido) tenga ese método y que sin embargo, solo se pueda ejecutar mientras el objeto está en "Preparando el envío".

Vayamos con el ejemplo:

~~~csharp
public class Pedido {
    protected IList<Producto> productos = new List<Producto>();

    public IList<Producto> Productos {
        get { return productos; }
    }

    protected EstadoPedido estadoPedido;

    public Pedido {
        estado = new PedidoEnCurso(this);
    }

    public void AgregaProducto(Producto producto) {
        estadoPedido.AgregaProducto(producto);
    }

    public void QuitaProducto(Producto producto) {
        estadoPedido.QuitaProducto(producto);
    }

    public void QuitaTodo() {
        estadoPedido.QuitaTodo()
    }

    public void EstadoSiguiente() {
        estadoPedido = estadoPedido.EstadoSiguiente();
    }

    public void Imprime() {
        Console.WriteLine("Contenido del pedido:");
        foreach(var producto in Productos) {
            producto.Imprime();
        }
        Console.WriteLine();
    }
}

public abstract class EstadoPedido {
    protected Pedido pedido;

    public EstadoPedido(Pedido pedido) {
        this.pedido = pedido;
    }

    public abstract void AgregaProducto(Producto producto);
    public abstract void QuitaTodo();
    public abstract void QuitaProducto(Producto producto);
    public abstract EstadoPedido EstadoSiguiente();
}

public class PedidoEnCurso : EstadoPedido {
    public PedidoEnCurso(Pedido pedido) : base(pedido) {}

    public override void AgregaProducto(Producto producto) {
        pedido.Productos.Add(pedido);
    }

    public override void QuitaTodo() {
        pedido.Productos.Clear();
    }

    public override void QuitaProducto(Producto producto) {
        pedido.Productos.Remove(pedido);
    }

    public override EstadoPedido EstadoSiguiente() {
        return new PedidoConfirmado(pedido);
    }
}

public class PedidoConfirmado : EstadoPedido {
    public PedidoConfirmado(Pedido pedido) : base(pedido) {}

    public override void AgregaProducto(Producto producto) {}

    public override void QuitaTodo() {
        pedido.Productos.Clear();
    }

    public override void QuitaProducto(Producto producto) {}

    public override EstadoPedido EstadoSiguiente() {
        return new PedidoEntregado(pedido);
    }
}

public class PedidoEntregado : EstadoPedido {
    public PedidoEntregado(Pedido pedido) : base(pedido) {}

    public override void AgregaProducto(Producto producto) {}

    public override void QuitaTodo() {}

    public override void QuitaProducto(Producto producto) {}

    public override EstadoPedido EstadoSiguiente() {
        return this;
    }
}

public class Producto {
    protected string nombre;

    public Producto(string nombre) {
        this.nombre = nombre;
    }

    public void Imprime() {
        Console.WriteLine($"Producto: {nombre}");
    }
}

public class Usuario {
    static void Main(string[] args) {

        Pedido pedido = new Pedido();
        pedido.AgregaProducto(new Producto("Book 1"));
        pedido.AgregaProducto(new Producto("Book 2"));
        pedido.Imprime();
        pedido.EstadoSiguiente();
        pedido.AgregaProducto(new Producto("Book 3"));
        pedido.QuitarTodo();
        pedido.Imprime();

        Pedido pedido2 = new Pedido();
        pedido2.AgregaProducto(new Producto("Book 10"));
        pedido2.AgregaProducto(new Producto("Book 20"));
        pedido2.Imprime();
        pedido2.EstadoSiguiente();
        pedido2.Imprime();
        pedido2.EstadoSiguiente();
        pedido2.QuitarTodo(); //En este estado no hará nada
        pedido2.Imprime();
    }
}
~~~