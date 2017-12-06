---
layout: post
title: Patrón Facade
tags: Arquitectura
---

La función del patrón facade es resolver agrupando en una única interfaz como conjunto de objetos varias interfaces.

De esta forma el patrón facade encapsula las interfaces especificas y expone una unica interfaz como punto de entrada.

Para los mortales, simplemente se trata de que toda petición entre por una interfaz que engloba las demás y esta sea capaz de redirigir hacia la interfaz concreta que tiene el servicio al que esta solicitando acceso la petición.

Una vez más, vamos con el ejemplo para clarificar.

En nuestro sistema de libros tenemos un servicio web para mostrar toda el site. Sin embargo, en la arquitectura del site hemos divido los servicios por las entidades con las que trabaja. De esta forma, tendremos un servicio que trate el catálago, otro que trate los libros y otro que trate los pedidos.

~~~csharp
public interface ICatalagoService {
    void GetCatalogo();
}

public interface IBookService {
    void GetBookById(Guid book);
}

public interface IPedidosService {
    void GetPedidoById(Guid Pedido);
}

public class CatalogoService : ICatalagoService {
    public void GetCatalogo() {
        Console.WriteLine("Contenido del Catalógo");
    }
}

public class BookService : IBookService {
    public void GetBookById(Guid id) {
        Console.WriteLine($"Datos del libro: {id}");
    }
}

public class PedidosService : IPedidosService {
    public void GetPedidoById(Guid id) {
        Console.WriteLine($"Datos del pedido: {id}");
    }
}

public interace IFacadeService {
    void GetCatalogo();
    void GetBookById(Guid id);
    void GetPedidoById(Guid id);
}

public class FacadeService : IFacadeService {
    private readonly ICatalagoService _catalogo = new CatalagoService();
    private readonly IBookService _book = new BookService();
    private readonly IPedidosService  _pedido= new PedidosService();

    public void GetCatalogo(){
        _catalogo.GetCatalogo();
    }

    public void GetBookById(Guid id) {
        _book.GetBookById(id)
    }

    public void GetPedidoById(Guid id) {
        _pedido.GetPedidoById(id);
    }
}

public class Web {
    static void Main(string[] args){
       IFacadeService _facade = new FacadeService();

       Console.WriteLine($"Mostrando Catalago {_facade.GetCatalogo}");
       var libro = _facade.GetBookById(a2ddedc8-8232-4eab-9fa4-1761a7e3ba22);

       Console.WriteLine($"Libro : {libro}");

       var pedido = _facade.GetPedidoById(a2ddedc8-8232-4eab-9fa4-1761a7e3ba23)

       Console.WriteLine($"Pedido : {pedido}");

    }
}
~~~

Saludos y hasta la próxima.