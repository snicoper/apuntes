.. _reference-programacion-csharp-new_and_override:

#######################
new and override basico
#######################

Fuentes
*******

* http://msdn.microsoft.com/es-es/library/ms173153.aspx

Cuando usar new y cuando usar virtual/override.

Supongamos que tenemos 2 clases

.. code-block:: c#

    class A
    {
        public void MethodA()
        {
            Console.WriteLine("Metodo en clase A");
        }

        // Es lo mismo que:
        // public virtual void MethodA()
        // {
            // Console.WriteLine("Metodo en clase A");
        // }
    }

    class B : A
    {
        public new void MethodA()
        {
            Console.WriteLine("Metodo en clase B");
        }
    }

    class Test
    {
        public static void Main()
        {
            A a = new A();
            B b = new B();
            A ab = new B();

            a.MethodA(); // Metodo en clase A
            b.MethodA(); // Metodo en clase B
            ab.MethodA(); // Metodo en clase A
        }
    }

Ahora, si declaramos el método MethodA de la clase A como virtual y el MethodA de la clase B
como override, el resultado es el siguiente:

.. code-block:: c#

    class A
    {
        public virtual void MethodA()
        {
            Console.WriteLine("Metodo en clase A");
        }
    }

    class B : A
    {
        public override void MethodA()
        {
            Console.WriteLine("Metodo en clase B");
        }
    }

    class Test
    {
        public static void Main()
        {
            A a = new A();
            B b = new B();
            A ab = new B();

            a.MethodA(); // Metodo en clase A
            b.MethodA(); // Metodo en clase B
            ab.MethodA(); // Metodo en clase B
        }
    }

Con new, si una clase es downgradeada, mostrara el resultado del método base, en cambio
con override, lo sobrescribe siempre y muestra el valor de la clase derivada.
