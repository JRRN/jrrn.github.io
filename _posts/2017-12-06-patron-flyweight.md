---
layout: post
title: Patrón Flyweight
tags: Arquitectura
---
El patrón Flyweight esta enfocado a resolver el problema de la granularidad de los objetos.

Recordemos que la granularidad en programación es la capacidad de definir objetos fragmentando en unidades más pequeñas la composición de este objeto de la forma más correcta.

En nuestro caso de libros, pongamos el ejemplo de que a la hora de comprar un libro en formato papel, podemos elegir entre varias opciones, como por ejemplo que sea de tapa dura, de tapa blanda, que sea un libro de anillas, que el papel sea de 80 gramos, 90 gr o 100 gr (no tengo ni idea si estos valores son correctos).

Seguimos con el ejemplo para traducirlo a código:

~~~csharp

enum TipoLibro
{
    Anillas = 0,
    Encolado =1
}

public class OpcionLibro {
    protected string _tapa;
    protected int _grosorPapel;
    protected TipoLibro _tipoLibro;

    public OpcionLibro(TipoLibro tipoLibro){
        _tipoLibro = tipoLibro;
        _grosorPapel = getGrosorByTipoLibro(tipoLibro);
        _tapa = getTapaByTipoLibro(tipoLibro);
    }

    public void verOpcionesLibro(){
        Console.WriteLine($"Libro con {_tapa} y grosor de papel {_grosorPapel} para el tipo de libro selecionado {_tipoLibro}")
    }

    private int getGrosorByTipoLibro(int tipoLibro) {
        if(tipoLibro == 0) {
            return 80;
        }else if(tipoLibro == 1){
            return 100;
        }
        return 90; //default
    }

    private string getTapaByTipoLibro(int tipoLibro) {
        if(tipoLibro == 0) {
            return "blanda";
        }else if(tipoLibro == 1){
            return "dura";
        }
        return "blanda"; //default
    }
}

public class DeterminaOpcion {
    protected IDictionary<TipoLibro, OpcionLibro> opcionesLibro = new Dictionary<TipoLibro, OpcioLibro>();

    public OpcionLibro GetOpcionesLibro(TipoLibro tipoLibro) {
        resultadoTipoLibro = new OpcionLibro(tipoLibro);
    }
}




~~~