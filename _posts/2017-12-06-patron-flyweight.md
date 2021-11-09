---
layout: post
title: Patrón Flyweight
tags: Arquitectura
---
El patrón **Flyweight** está enfocado a resolver el problema de la granularidad de los objetos.

Recordemos que la granularidad en programación es la capacidad de definir objetos fragmentando en unidades más pequeñas la composición de este objeto de la forma más correcta.

En nuestro caso de libros, pongamos el ejemplo de que a la hora de comprar un libro en formato papel, podemos elegir entre varias opciones, como por ejemplo que sea de tapa dura, de tapa blanda, que sea un libro de anillas, que el papel sea de 80 gramos, 90 gr o 100 gr (no tengo ni idea si estos valores son correctos).

Seguimos con el ejemplo para traducirlo a código:

~~~csharp

enum TipoLibro
{
    Anillas = 0,
    Encolado =1
}

public class OpcionLibro
{
    protected string _tapa;
    protected int _grosorPapel;
    protected TipoLibroEnum _tipoLibro;

    public OpcionLibro(TipoLibroEnum tipoLibro)
    {
        _tipoLibro = tipoLibro;
        _grosorPapel = getGrosorByTipoLibro((int)tipoLibro);
        _tapa = getTapaByTipoLibro((int)tipoLibro);
    }

    public void VerOpcionesLibro()
    {
        Console.WriteLine(
            $"Libro con {_tapa} y grosor de papel {_grosorPapel} para el tipo de libro selecionado {_tipoLibro}");
    }

    private int getGrosorByTipoLibro(int tipoLibro)
    {
        switch (tipoLibro)
        {
            case 0:
                return 80;
            case 1:
                return 100;
        }

        return 90; //default
    }

    private string getTapaByTipoLibro(int tipoLibro)
    {
        switch (tipoLibro)
        {
            case 0:
                return "blanda";
            case 1:
                return "dura";
        }

        return "blanda"; //default
    }
}

public class DeterminaOpcion {
    protected IDictionary<TipoLibroEnum, OpcionLibro> opcionesLibro = new Dictionary<TipoLibroEnum, OpcionLibro>();

    public static OpcionLibro GetOpcionesLibro(TipoLibroEnum tipoLibro)
    {
        return new OpcionLibro(tipoLibro);
    }
}

public class LibroPedido{
    protected IList<OpcionLibro> opcionLibro = new List<OpcionLibro>();
    protected IList<int> precioVenta = new List<int>();

    public void agregaOpcionLibro(TipoLibroEnum tipoLibro, int precio, DeterminaOpcion opcion)
    {
        opcionLibro.Add(DeterminaOpcion.GetOpcionesLibro(tipoLibro));
        precioVenta.Add(precio);
    }

    public void MuestraOpciones()
    {
        var tamaño = opcionLibro.Count;

        for (int indice = 0; indice < tamaño; indice++)
        {
            opcionLibro[indice].VerOpcionesLibro();
            Console.WriteLine();
        }
    }
}

public class Cliente {
    static void Main(string[] args) {
        DeterminaOpcion opcion = new DeterminaOpcion();
        LibroPedido libroPedido = new LibroPedido();

        libropedido.agregaOpcionLibro(TipoLibro.Anillas, 10, opcion);
        libropedido.agregaOpcionLibro(TipoLibro.Encolado, 30, opcion);

        libroPedido.MuestraOpciones();
    }
}
~~~

Como se puede apreciar Flyweigth nos permite granular el tipo de libro y, sobre este, calcular las propiedades específicas del libro, tales como el grosor del papel y el tipo de tapa sin tener que pasar ningún parámetro sobre estos en cada capa del servicio.

Saludos.

