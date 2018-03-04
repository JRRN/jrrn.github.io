---
layout: post
title: Patrón Mediator
tags: Arquitectura
---
El patrón **Mediator** nos ayuda a gestionar y controlar las interacciones entre un conjunto de objetos sin que deban conocerse entre ellos.

Para los mortales, se define un objeto que tiene las reglas de interacción entre los objetos que se van a comunicar.

¿Todavía no? Veámoslo con un ejemplo:

Esta vez dejaremos a un lado los recurrentes ejemplos de nuestros libros para cambiar por algo más adaptable a nuestro ejemplo, "Torre de control, ¿me recibe?"

~~~csharp
public class TorreDeControl {
    private bool _pistaLlena = false;
    private int _numero;
    public void RecibeMensaje(int numero) {
        while ((_pistaLlena == true)) {
            try {
                Task.Delay(2000);
            }
            catch (Exception e) {
            }
        }
        _pistaLlena = true;
        _numero = numero;
    }
    public int EnviaMensaje() {
        while ((_pistaLlena == false)) {
            try {
                Task.Delay(2000);
            }
            catch (Exception e) {
            }
        }
        _pistaLlena = false;
        return _numero;
    }
}
public class Productor {
    private TorreDeControl _torreControl;
    private int _id;
    private static int num = 1;
    public Productor(TorreDeControl torreControl) {
        _torreControl = torreControl;
        _id = num++;
    }
    public void Run() {
        int num;
        while (true) {
        _torreControl.RecibeMensaje(new Random().Next(100, 999));
        Console.WriteLine($"p" {_id});
        }
    }
}
public class Consumidor {
    private TorreDeControl _torreControl;
    private int _id;
    private static int num = 1;
    public Consumidor(TorreDeControl torreControl) {
        _torreControl = torreControl;
        num++;
        _id = num;
    }
    public void Run() {
        while (true) {
            Console.WriteLine($"Consumidor {_id} {_torreControl.EnviaMensaje()}");
        }
    }
}
public class MediatorDemo {
  public static void main(string[] args) {
    TorreDeControl torreControl = new TorreDeControl();
    new Productor(torreControl).Run();
    new Productor(torreControl).Run();
    new Consumidor(torreControl).Run();
    new Consumidor(torreControl).Run();
    new Consumidor(torreControl).Run();
    new Consumidor(torreControl).Run();
  }
}
~~~