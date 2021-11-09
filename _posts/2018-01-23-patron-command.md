---
layout: post
title: Patrón Command
tags: Arquitectura
---
El patrón **Command** nos ayuda a transformar una solicitud en un objeto. Estas solicitudes tienen la propiedad de poder encolarse, ser borradas y actualizadas dentro de la cola de peticiones.

Volviendo a nuestro caso de libros, todos sabemos que ciertos libros en IT son altamente propensos a quedarse obsoletos, para ello, nuestra implementación de tienda, es capaz de emitir una rebaja para aquellos libros que no están teniendo la salida que queremos. Este proceso, se podría hacer manual con un campo de rebaja, pero queremos que sea el sistema el que emita esta rebaja según la premisa de que si no se vende rebájalo tantas veces como sea necesario hasta salir del stock.

Para ello, el patrón command nos ayudará a no tener que efectuar este proceso por cada uno de los libros del stock.

~~~csharp
public class Book {
    protected string _nombre;
    protected DateTime _fechaEntradaStock;
    protected double _precioVenta;

    public Book(string nombre, DateTime fechaEntradaStock, double precioVenta) {
        _nombre = nombre;
        _fechaEntradaStock = fechaEntradaStock;
        _precioVenta = precioVenta;
    }

    public long TiempoStock(){
        return (DateTime.Now - _fechaEntradaStock).Ticks;
    }

    public void ActualizaPrecio(double descuento) {
            _precioVenta = 0.01 * Math.Round(descuento) * _precioventa *100;
    }

    public void Ver() {
        Console.WriteLine($"{nombre} tiene un precio {_precioVenta} entrada {_fechaEntradaStock}");
    }
}

public class AplicarRebaja {
    protected IList<Book> _stockLibros = new List<Book>();
    protected long _hoy;
    protected long _tiempoStock;
    protected double _descuento;

    public AplicarRebaja(long tiempoStock, double descuento) {
        _hoy = DateTime.Now.Ticks;
        _tiempoStock = tiempoStock;
        _descuento = descuento;
    }

    public void Rebajar(IList<Book> Libros) {
        _stockLibros.Clear();
        foreach(var libro in Libros) {
            if(libro.TiempoStock()) >= _tiempoStock{
                _stockLibros.Add(libro);
            }
        }
        foreach(var libroARebajar in _stockLibros){
            libroARebajar.ActualizaPrecio(1.0 - descuento);
        }
    }

    public void Anular() {
        foreach(var libro in _stockLibros) {
            libro.ActualizaPrecio(1.0 / (1.0 - descuento));
        }
    }

    public void Restablecer(){
        foreach(var libro in _stockLibros) {
            libro.ActualizaPrecio(1.0 - descuento));
        }
    }
}

public class Catalogo {
    protected IList<Book> _stockLibros = new List<Book>();
    protected IList<AplicarRebaja> commands = new List<AplicarRebaja>();

    public void commandRebaja(AplicarRebaja aplicarRebaja) {
        commands.Insert(0, aplicarRebaja);
        aplicarRebaja.Rebajar(_stockLibros);
    }

    public void commandAnulaRebaja(int commandNum){
        commands[commandNum].Anular();
    }

    public void restablecerSolicitudRebaja() {
        commands[commandNum].Restablecer();
    }

    public void agrega(Book libro) {
        _stockLibros.Add(libro);
    }

    public void visualiza() {
        foreach (Book libro in _stockLibros) {
            libro.Ver();
        }
    }
}
~~~