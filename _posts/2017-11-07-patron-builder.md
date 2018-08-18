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
        public abstract void agregaDocumento(string documento);
        public abstract void imprime();
    }

    public class DocumentacionHtml : Documentacion
    {
        public override void agregaDocumento(string documento)
        {
            if (documento.StartsWith("HTML", StringComparison.Ordinal)) contenido.Add(documento);
        }

        public override void imprime()
        {
            Console.WriteLine("Documentación HTML");
            foreach (string s in contenido) Console.WriteLine(s);
        }
    }

    public class DocumentacionPdf : Documentacion
    {
        public override void agregaDocumento(string documento)
        {
            if (documento.StartsWith("PDF", StringComparison.Ordinal)) contenido.Add(documento);
        }

        public override void imprime()
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

        public override void construyeSolicitudPedido(string nombreCliente)
        {
            string documento;
            documento = $"Solicitud de pedido Cliente: {nombreCliente} HTML";
            documentacion.agregaDocumento(documento);
        }

        public override void construyeSolicitudFactura(string nombreSolicitante)
        {
            string documento;
            documento = $"HTML Solicitud de factura Solicitante:  {nombreSolicitante}";

            documentacion.agregaDocumento(documento);
        }
    }

    public class ConstructorDocumentacionPdf : ConstructorDocumentacion
    {
        public ConstructorDocumentacionPdf()
        {
            documentacion = new DocumentacionPdf();
        }

        public override void construyeSolicitudPedido(string nombreCliente)
        {
            string documento;
            documento = "<PDF>Solicitud de pedido Cliente: " + nombreCliente + "</PDF>";
            documentacion.agregaDocumento(documento);
        }

        public override void construyeSolicitudFactura(string nombreSolicitante)
        {
            string documento;
            documento = "<PDF>Solicitud de factura Solicitante: " + nombreSolicitante + "</PDF>";
            documentacion.agregaDocumento(documento);
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
~~~

Saludos.
