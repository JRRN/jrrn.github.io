---
layout: post
title: Patrón Interpreter
tags: Arquitectura
---
El patrón **Interpreter** nos proporciona la utilidad de transformar, la gramática del lenguaje, de tal forma que podamos evaluar, condificando estas expresiones del lenguaje natural, en objetos.

En resumidas, nos da la facilidad de transformar el lenguaje que hablamos y con el que nos comunicamos, en lenguaje máquina.

Y no, esto no es Inteligencia Artificial.

Vamos con el ejemplo.

En nuestro catálogo de libros nos gustaría implementar un buscador que a partir de expresiones regulares, nos devuelva unos y/u otros resultados.

~~~csharp
public abstract class Expression {
    public abstract bool Validate(string descripcion);

    protected static string origen;
    protected static int position;
    protected static string libro;

    protected static void NextBook() {
        while ((position < origen.Length) && (origen[position] ==  ' ')) {
            position++;
            if(indice == origen.Length){
                libro = null;
            } else if((origen[position] == '(') || (origen[position] == ')')) {
                libro = origen.Substring(position,1);
                position++;
            } else {
                int initPosition = position;
                 while ((position < origen.Length) && (origen[position] !=  ' ') && (origen[position] != ')') {
                     position++;
                     libro = origen.Substring(initPosition, position -initPosition)
            }
        }
    }

    public static Expression Analize(strin origen) {
        Expresion.origen = origen;
        position = 0;
        NextBook();
        return OperatorX.Parse();
    }

    public static Expresion Parse() {
        Expresion result;
        if (libro == "(") {
            NextBook();
            result = OperatorX.Parse();
            if (libro == null)
                throw new Exception("Error de sintaxis");
            if (libro != ")")
                throw new Exception("Error de sintaxis");
            NextBook();
        }
        else {
            result = PalabraClave.Parse();
        }
        return result;
    }
}

public class Word : Expresion
{
    protected string _word;

    public Word(string word)
    {
        this._word = word;
    }

    public override bool Eval(string descripcion)
    {
        return descripcion.IndexOf(_word) != -1;
    }

    public static new Expresion Parse() {
        Expresion result;
        result = new Word(pieza);
        NextBook();
        return result;
    }
}

public abstract class BinaryOperator : Expresion
{
    protected Expresion _leftOperator, _rightOperator;

    public BinaryOperator(Expresion leftOperator, Expresion rightOperator) {
        _leftOperator = leftOperator;
        _rightOperator = rightOperator;
    }
}

public class OperatorX : BinaryOperator {
    public OperatorX(Expresion leftOperator, Expresion rightOperator)
           : base(leftOperator, rightOperator) { }

    public override bool evalua(string descripcion) {
        return leftOperator.Eval(descripcion) || rightOperator.Eval(descripcion);
    }

    public static new Expresion Parse()
    {
        Expresion leftResult, RightResult;
        leftResult = OperatorY.Parse();
        while ((libro != null) && (libro == "o")) {
           NextBook();
           RightResult = OperatorY.Parse();
           leftResult = new OperatorX(leftResult, RightResult);
        }
        return leftResult;
    }
}

public class OperatorY : BinaryOperator {
    public OperatorY(Expresion leftOperator, Expresion rightOperator)
           : base(leftOperator, rightOperator) { }

    public override bool Eval(string descripcion) {
        return leftOperator.Eval(descripcion) && rightOperator.Eval(descripcion);
    }

    public static new Expresion Parse() {
        Expresion leftResult, RightResult;
        leftResult = Expresion.Parse();
        while ((pieza != null) && (pieza == "y")) {
           NextBook();
           RightResult = Expresion.Parse();
           leftResult = new OperatorY(leftResult, RightResult);
        }
        return leftResult;
    }
}

public class User {
    static void Main(string[] args) {
        Expresion expresionConsulta = null;
        Console.Write("Introduzca su consulta: ");
        string consulta = Console.ReadLine();
        try {
            expresionConsulta = Expresion.Analize(consulta);
        } catch (Exception e) {
            Console.WriteLine(e.Message);
            expresionConsulta = null;
        }
        if (expresionConsulta != null) {
            Console.WriteLine("Introduzca la descripción de un libro: ");
            string descripcion = Console.ReadLine();
            if (expresionConsulta.Eval(descripcion))
                Console.WriteLine("La descripción responde a la consulta");
            else
                Console.WriteLine("La descripción no responde a la consulta");
        }
    }
}
~~~

Y la salida que obtendríamos sería:

Introduzca su consulta: (it o historia) y actualizado y Pdf

Introduzca la descripción de un libro:

Este libro de it que es un Pdf esta actualizado

La descripción responde a la consulta

Saludos.
