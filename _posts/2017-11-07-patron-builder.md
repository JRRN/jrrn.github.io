---
layout: post
title: Patrón Builder
tags: Arquitectura
---

El objetivo del patrón **Builder** es abstraer la construcción de objetos complejos de su implementación de modo que un cliente pueda crear objetos complejos sin tener que preocuparse de las diferencias en su implantación.

Volviendo a nuestro ejemplo de los libros y revistas. Durante la compra de libros/revistas se generan varios documentos como la solicitud del pedido y la factura.

Estos documentos se pueden generar en pdf y/o en formato html para remitir por mail, por ejemplo. Con lo que obtendríamos los métodos constructorDocumentacionHtml y constructorDocumentacionPdf.

~~~csharp
    public abstract class Documentacion
    {
        protected IList<string> contenido = new List<string>();
        public abstract void AgregaDocumento(string documento);
        public abstract void Imprime();
    }

    public class DocumentacionHtml : Documentacion
    {
        public override void AgregaDocumento(string documento)
        {
            if (documento.StartsWith("HTML", StringComparison.Ordinal)) contenido.Add(documento);
        }

        public override void Imprime()
        {
            Console.WriteLine("Documentación HTML");
            foreach (string s in contenido) Console.WriteLine(s);
        }
    }

    public class DocumentacionPdf : Documentacion
    {
        public override void AgregaDocumento(string documento)
        {
            if (documento.StartsWith("PDF", StringComparison.Ordinal)) contenido.Add(documento);
        }

        public override void Imprime()
        {
            Console.WriteLine("Documentación PDF");
            foreach (string s in contenido) Console.WriteLine(s);
        }
    }

    public abstract class ConstructorDocumentacion
    {
        protected Documentacion documentacion;
        public abstract void construyeSolicitudPedido(string nombreCliente);
        public abstract void construyeSolicitudFactura(string nombreSolicitante);
        public Documentacion resultado()
        {
            return documentacion;
        }
    }

    public class ConstructorDocumentacionHtml : ConstructorDocumentacion
    {
        public ConstructorDocumentacionHtml()
        {
            documentacion = new DocumentacionHtml();
        }

        public override void ConstruyeSolicitudPedido(string nombreCliente)
        {
            string documento;
            documento = $"Solicitud de pedido Cliente: {nombreCliente} HTML";
            documentacion.AgregaDocumento(documento);
        }

        public override void ConstruyeSolicitudFactura(string nombreSolicitante)
        {
            string documento;
            documento = $"HTML Solicitud de factura Solicitante:  {nombreSolicitante}";

            documentacion.AgregaDocumento(documento);
        }
    }

    public class ConstructorDocumentacionPdf : ConstructorDocumentacion
    {
        public ConstructorDocumentacionPdf()
        {
            documentacion = new DocumentacionPdf();
        }
        public override void ConstruyeSolicitudPedido(string nombreCliente)
        {
            string documento;
            documento = $"<PDF>Solicitud de pedido Cliente: {nombreCliente} </PDF>";
            documentacion.AgregaDocumento(documento);
        }

        public override void ConstruyeSolicitudFactura(string nombreSolicitante)
        {
            string documento;
            documento = $"<PDF>Solicitud de factura Solicitante: {nombreSolicitante}</PDF>";
            documentacion.AgregaDocumento(documento);
        }
    }

    public class Vendedor
    {
        protected ConstructorDocumentacion constructor;

        public Vendedor(ConstructorDocumentacion constructor)
        {
            this.constructor = constructor;
        }

        public Documentacion construye(string nombreCliente)
        {
            constructor.construyeSolicitudPedido(nombreCliente);
            constructor.construyeSolicitudFactura(nombreCliente);
            Documentacion documentacion = constructor.resultado();
            return documentacion;
        }
    }
    
    public class Usuario {
    static void Main(string[] args) {
        ConstructorDocumentacion constructor;
        Console.WriteLine("Desea generar " + "documentación HTML (1) o PDF (2):");
        string seleccion = Console.ReadLine();
        if (seleccion == "1") {
            constructor = new ConstructorDocumentacionHtml();
        } else {
            constructor = new ConstructorDocumentacionPdf();
        }
        Vendedor vendedor = new Vendedor(constructor);
        Documentacion documentacion = vendedor.Construye("JRRN");
        documentacion.Imprime();
    }
}
~~~

Saludos.
