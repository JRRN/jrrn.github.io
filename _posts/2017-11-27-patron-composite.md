---
layout: post
title: Patrón Composite
tags: Arquitectura
---

El patrón **composite** nos da la utilidad de generar una composición de objetos variables. Esta composición, generalmente, se encuentra en forma de árbol y respeta una jerarquía.

A través de este polimorfismo variable de la citada jerarquía el encapsulamiento a ojos del cliente es muy sencilla y puede usarlos sin tener que conocer la profundidad del arbol y objetos generados.

En nuestro caso de la venta de libros, el supuesto donde aplicaríamos este patrón podrái ser en la distribucción de nuestro repositorio, tanto a clientes finales, como a editoriales más pequeñas, que pueden tener clientes.

Sin más, vamos al ejemplo con el que se verá más claro su estrucutura y comportamiento:

~~~csharp
public abstract class Cliente {
    protected static double _costeLibroUnitario = 1.0;
    protected int _numeroLibros;

    public void anadirLibro(){
        _numeroLibros += 1;
    }

    public abstract double calcularPedido();
    public abstract bool agregarEditorial(string nombreClienteEditorial);
}

public class ClienteFinal : Cliente {
    public override double calcularPedido() {
        return _numeroLibros * _costeLibroUnitario;
    }
    public override bool agregarEditorial(Cliente cliente) {
        return false;
    }
}

public class EditorialCliente : Cliente {
    protected List<Cliente> _clientesEditorial = new List<Cliente>();

    public override double calcularPedido(){
        double total = 0.0;

        foreach(Cliente clienteEditorial in _clientesEditorial){
            total = total + clienteEditorial.calcularPedido();
        }
        return total + _numeroLibros * _costeLibroUnitario;
    }

    public override bool agregarCliente(Cliente cliente) {
        _clientesEditorial.Add(cliente);
        return true;
    }
}

public class Pedido {
    static void Main(string[] args) {
        Cliente clienteFinal = new ClienteFinal();
        clienteFinal.agregarEditorial();

        Cliente otroClienteFinal = new ClienteFinal();
        otroClienteFinal.agregarEditorial();
        otroClienteFinal.anadirLibro();

        Editorial editorialCliente = new EditorialCliente();
        editorialCliente.agregarCliente(clienteFinal);
        editorialCliente.agregarCliente(otroClienteFinal);
        editorialCliente.anadirLibro();

        Console.WriteLine("$Total pedidos clientes: { editorialCliente.calcularPedido() }");
}
~~~

El resultado que obtendremos será el calculo de los libro solicitados por los clientes.

Saludos.

