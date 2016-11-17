.. _reference-programacion-csharp-virtual:

##########
C# Virtual
##########

Fuentes
*******

* http://msdn.microsoft.com/es-es/library/9fkccyh4.aspx

-------------------

La palabra clave virtual se utiliza para modificar un método,
propiedad, indizador o  declaración de evento y permite invalidar cualquiera
de estos elementos en una clase derivada.

No puede utilizar el modificador virtual con los modificadores static, abstract,
private u override.

Para poder sobre-escribir un método (por ejemplo) en una subclase, es necesario
que la clase padre tenga declarado un virtual.

Por ejemplo

.. code-block:: c#

    class A {
        public void Mostrar() {}
    }

    class B : A {
        public override void Mostrar() {}
    }

La class B daría error, por que el método Mostrar() en la clase A, no se deja
sobre-escribir, para poder hacerlo, vasta con declarar el método de la clase A
como virtual.

.. code-block:: c#

    class A {
        public virtual void Mostrar() {}
    }

    class B : A {
        public override void Mostrar() {}
    }

Cuando simplemente se quiere "sobre-escribir un método padre":

.. code-block:: c#

    class A {
        public virtual void Mostrar() {}
    }

    class B : A {
        public new void Mostrar() {}
    }

Ver :ref:`reference-programacion-csharp-new_and_override` , para ver las diferencias entre new y override.
