---
layout: post
title: Patrón Prototype
tags: Arquitectura
---

El objetivo de este patrón es la creación de nuevos objetos mediante la duplicación de objetos existentes llamados prototipos que disponen de la capacidad de clonación.

En resumen, y simplificando, crear nuevos objetos a partir de un objeto existente sin modificar una clase siempre que se añada un nuevo objeto.

En nuestro ejemplo de libros, a la hora de generar los documentos digitales de un pedido, podemos reutilizar la clase que genera la primera instancia del objeto libro digital para crear tantos libros digitales, el pedido y la factura y luego volcar en ellos cada uno de su contenido.

Veamos a ver cómo quedará el código:

~~~csharp
public abstract class Documento
{
    protected string contenido = "";

    public Documento Duplica()
    {
        var resultado = (Documento)MemberwiseClone();
        return resultado;
    }

    public void Rellena(string informacion)
    {
        contenido = informacion;
    }

    public abstract void Imprime();
    public abstract void Visualiza();
}

public abstract class DocumentoDigital
{
    protected string _contenido = String.Empty;
    public DocumentoDigital Duplica()
    {
        var resultado = (DocumentoDigital)MemberwiseClone();
        return resultado;
    }
    public void Rellena(string contenido)
    {
        _contenido = contenido;
    }
    public abstract void Genera();
    public abstract void Visualiza();
}

public abstract class Documentos
{
    public IList<Documento> documentos { get; protected set; }
}

public class DocumentosVacios : Documentos
{
    public static DocumentosVacios _instance = null;
    private DocumentosVacios()
    {
        documentos = new List<Documento>();
    }
    public static DocumentosVacios Instance()
    {
        return _instance ?? (_instance = new DocumentosVacios());
    }
    public void Incluye(Documento doc) { documentos.Add(doc); }
    public void Excluye(Documento doc) { documentos.Remove(doc); }
}

public class DocumentosCliente : Documentos
{
    public DocumentosCliente(string informacion)
    {
        documentos = new List<Documento>();
        DocumentosVacios documentosVacios = DocumentosVacios.Instance();
        IList<Documento> documentoVacios = documentosVacios.documentos;

        foreach (Documento docs in documentoVacios)
        {
            Documento copioDocumento = docs.Duplica();
            copioDocumento.Rellena(informacion);
            documentos.Add(copioDocumento);
        }
    }
    public void Visualiza()
    {
        foreach (Documento documento in documentos)
        {
            documento.Visualiza();
        }
    }
    public void Imprime()
    {
        foreach (Documento documento in documentos)
        {
            documento.Visualiza();
        }
    }
}

public class FacturaPrototype : Documento
{
    public override void Visualiza()
    {
        Console.WriteLine($"Factura: {contenido}");
    }
    public override void Imprime()
    {
        Console.WriteLine($"Imprime Factura: {contenido}");
    }
}

public class LibroDigital : Documento
{
    public override void Visualiza()
    {
        Console.WriteLine($"LibroDigital: {contenido}");
    }
    public override void Imprime()
    {
        Console.WriteLine($"Imprime LibroDigital: {contenido}");
    }
}

public class PedidoPrototype : Documento
{
    public override void Visualiza()
    {
        Console.WriteLine($"Pedido: {contenido}");
    }
    public override void Imprime()
    {
        Console.WriteLine($"Imprime Pedido: {contenido}");
    }
}
~~~

Para finalizar veremos las salida con una clase Usuario:

~~~csharp
public class Usuario{
    static void Main(string[] args)  {
        DocumentosVacios documentosVacios = DocumentosVacios.Instance();
        documentosVacios.Incluye(new PedidoPrototype());
        documentosVacios.Incluye(new FacturaPrototype());
        documentosVacios.Incluye(new LibroDigital());
        DocumentosCliente documentoCliente = new DocumentosCliente("Un usuario");
        DocumentosCliente documentoCliente2 = new DocumentosCliente("Otro Usuario");
        documentoCliente.Visualiza();
        documentoCliente2.Visualiza();
    }
}
~~~

Saludos.


