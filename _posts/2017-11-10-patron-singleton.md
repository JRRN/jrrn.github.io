---
layout: post
title: Patrón Singleton
tags: Arquitectura
---

El patrón **singleton** tiene como objetivo asegurar que una clase sólo posee una instancia y proporciona un método de clase único que devuelve la instancia.

Es un patrón simple y conocido. Si queremos que solo haya una instancia de un objeto y no se puedan generar más mientras haya una existente, este es nuestro patrón. Por ejemplo, si recordamos el patrón Abstract Factory, solo necesitamos una única instancia para ir generando los demás tipos de libros.

En nuestro ejemplo de libros, gestionaremos las clases que deban tener una sola instancia:

~~~csharp
    public class DocumentosVacios : Documentos {
    public static DocumentosVacios _instance = null;
    private DocumentosVacios() {
        documentos = new List<Documento>();
    }
    public static DocumentosVacios Instance() {
        if(_instance == null) {
            _instance = new DocumentosVacios();
        }
    }
    public void Incluye(Documento doc) {
        documentos.Add(doc);
    }
    public void Excluye(Documento doc) {
        documentos.Remove(doc);
    }
}
~~~

O si creamos una nueva clase Editorial en la que inicializaremos los datos de la editorial una vez y los recuperaremos siempre de esa misma instancia sin tener que generar una instancia cada vez que queramos recuperar los datos de la editorial:

~~~csharp
    public class EditorialSingleton {
        public string nombreEditorial  { get; set; }
        public string ubicacion  { get; set; }
        public DateTime fechaEditorial  { get; set; }
        private static EditorialSingleton _instance = null;

        private EditorialSingleton() { }
        public static EditorialSingleton Instance() => _instance ?? (_instance = new EditorialSingleton());

        public void Visualiza()
        {
            Console.WriteLine($"Editorial:  {nombreEditorial}");
            Console.WriteLine($"Ubicacion:  {ubicacion}");
        }
}
~~~

Para ver la salida:

~~~csharp
    public class TestEditorial {
    static void Main(string[] args) {
        EditorialSingleton laEditorial = EditorialSingleton.Instance();
        laEditorial.nombreEditorial = "JRRN Publicaciones";
        laEditorial.ubicacion = "Barcelona";
        laEditorial.fechaEditorial = new DateTime(2018,05,11);

        EditorialSingleton _laEditorial = EditorialSingleton.Instance();
        _laEditorial.Visualiza();
    }
}
~~~


