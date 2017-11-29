---
layout: post
title: Patrón Prototype
tags: Arquitectura
---

El objetivo de este patrón es la creación de nuevos objetos mediante la duplicación de objetos existentes llamados prototipos que disponen de la capacidad de clonación.

En resumen, y simplificando, crear nuevos objetos a partir de un objeto existente sin modificar una clase siempre que se añada un nuevo objeto.

En nuestro ejemplo de libros, a la hora de generar los documentos digitales de un pedido, podemos reutilizar la clase que genera la primera instancia del objeto libro digital para crear tantos libros digitales, el pedido y la factura y luego volcar en ellos cada uno de su contenido.

Veamos a ver como quedará el código:

~~~csharp
public abstract class DocumentoDigital {
    protected string _contenido = String.Empty();
    public DocumentoDigital Duplica() {
        DocumentoDigital resultado;
        resultado = (DocumentoDigital) this.MemberwiseClone();
        return resultado;
    }
    public void Rellena(string contenido) {
        _contenido = contenido
    }
    public abstract void Genera();
    public abstract void Visualiza();
    }
    public class Factura : Documento {
        public override void visualiza() {
            Console.WriteLine($"Factura: {contenido}")
        }
        public override void Imprime() {
            Console.WriteLine($"Imprime Factura: {contenido}")
        }
    }
    public class Pedido : Documento {
        public override void Visualiza() {
            Console.WriteLine($"Pedido: {contenido}")
        }
        public override void Imprime()  {
            Console.WriteLine($"Imprime Pedido: {contenido}")
        }
    }
    public class LibroDigital : Documento {
        public override void Visualiza() {
            Console.WriteLine($"LibroDigital: {contenido}")
        }
        public override void Imprime() {
            Console.WriteLine($"Imprime LibroDigital: {contenido}")
        }
    }
}
~~~

Una vez definidas las clases de cada uno de los objetos, definiremos la clases Documentos:

~~~csharp
public abstract class Documentos{
    public IList<Documento> documentos { get; protected set; }
}
public abstract class Documentos {
    public IList<Documento>;
    documentos { get; protected set; }
}
public class DocumentosVacios : Documentos {
    public static DocumentosVacios _instance = null;
    private DocumentosVacios()  {
        documentos = new List<Documento>();
    }
    // Patrón Singleton
    public static DocumentosVacios Instance() {
        if(_instance == null) {
            _instance = new DocumentosVacios();
    }
    return _instance;
    }
    public void Incluye(Documento doc) { documentos.Add(doc);  }
    public void Excluye(Documento doc) { documentos.Remove(doc);  }
}
~~~

Y ahora la clase DocumentosCliente:

~~~csharp
public class DocumentosCliente : Documentos {
    public DocumentosCliente(string informacion) {
        documentos = new List<Documento>();
        DocumentosVacios documentosVacios = new DocumentosVacios.Instance();
        IList<Documento> documentosVacios = documentosVacios.documentos;

        foreach(Documento documentos in documentosVacios) {
            Documento copioDocumento = documento.Duplica();
            copioDocumento.Rellena(informacion);
            documentos.Add(copioDocumento)
        }
    }
    public void Visualiza() {
        foreach(Documento documento in documentos) {
            documento.Visualiza();
        }
    }
    public void Imprime() {
        foreach(Documento documento in documentos) {
            documento.Imprime();}
        }
    }
}
~~~

Para finalizar veremos las salida con una clase Usuario:

~~~csharp
public class Usuario{
    static void Main(string[] args)  {
        DocumentosVacios documentosVacios = DocumentosVacios.Instance();
        documentosVacios.Incluye(new Pedido);
        documentosVacios.Incluye(new Factura);
        documentosVacios.Incluye(new LibroDigital);
        DocumentosCliente JR = new DocumentosCliente("JR");
        DocumentosCliente RN = new DocumentosCliente("RN");
        JR.Visualiza();
        RN.Visualiza();
    }
}
~~~

Saludos.