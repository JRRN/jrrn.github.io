---
layout: post
title: Patrón Visitor
tags: Arquitectura
---

El patrón Visitor nos permite agregar operaciones a objetos sin tener que modificar la clase concreta de estos objetos. Su uso se recomienda para pequeñas y pocas funcionalidades extra.



~~~csharp
public inteface Visitante {
    void visita(EditorialSinFilial editorialSinFilial);
    void visita(EditorialMadre editorialMadre);

}

public abstract class Editorial {
    public string nombre { get; protected set; }
    public string email { get; protected set; }
    public string direccion { get; protected set; }

    public Editorial(string nombre, string email, string direccion) {
        this.nombre = nombre;
        this.email = email;
        this.direccion = direccion;
    }

    public abstract bool AgregarEditorialFilial(Editorial filial);

    public abstract void AceptaVisitante(Visitante visitante);
}

public class EditorialSinFilial : Editorial {
    public EditorialFilial(string nombre, string email, string direccion)
            :base (string nombre, string email, string direccion) { }

    public abstract bool AgregarEditorialFilial(Editorial filial) {
        return false;
    }

    public abstract void AceptaVisitante(Visitante visitante) {
        visitante.visita(this);
    }
}

public class EditorialMadre : Editorial {
    protected IList<Editorial> editorialesFiliales = new List<Editorial>();

    public EditorialMadre(string nombre, string email, string direccion)
            :base (string nombre, string email, string direccion) { }

    public abstract bool AgregarEditorialFilial(Editorial filial) {
        editorialesFiliales.Add(filial);
        return true;
    }

    public abstract void AceptaVisitante(Visitante visitante) {
        visitante.visita(this);
        foreach(Editorial editorialFilial in editorialesFiliales) {
            filial.AceptaVisitante(visitante);
        }
    }
}

public class VisitanteMailingComercial : Visitante {
    public void visita(EditorialSinFilial editorial) {
        Console.WriteLine($"Envía mail a {editorial.nombre} a {editorial.email}");
    }
       public void visita(EditorialMadre editorial) {
        Console.WriteLine($"Envía mail a {editorial.nombre} a {editorial.email}");
    }
}

public class Usuario {
    static void Main(string[] args) {
        Editorial editorial1 = new EditorialSinFilial("empresa1","mail@empresa1.com","Calle Empresa 1");
        Editorial editorial2 = new EditorialSinFilial("empresa2","mail@empresa2.com","Calle Empresa 2");

        Editorial grupoEditorial = new EditorialMadre("grupoEditorial1","mail@grupoEditorial1.com","Calle Grupo Editorial1"):

        grupoEditorial.AgregarEditorialFilial(editorial1);
        grupoEditorial.AgregarEditorialFilial(editorial2);

        Editorial editorial3 = new EditorialSinFilial("empresa3","mail@empresa3.com","Calle Empresa 3");

        Editorial grupoEditorial2 = new EditorialMadre("grupoEditorial2","mail@grupoEditorial2.com","Calle Grupo Editorial2");

        grupoEditorial2.AgregarEditorialFilial(grupoEditorial);
        grupoEditorial2.AgregarEditorialFilial(editorial3);

        grupoEditorial2.AceptaVisitante(new VisitanteMailingComercial());
    }
}
~~~

Saludos.
