.. _reference-programacion-csharp-csharp_script-lanzar_finalizador_csharp:

##############################
Lanzar Finalizador de Clase C#
##############################

Fuentes
*******

* http://stackoverflow.com/a/1987288
* http://msdn.microsoft.com/es-es/library/system.idisposable.dispose%28v=vs.110%29.aspx
* http://canyouhearthebits.wordpress.com/2008/08/08/como-implementar-correctamente-idisposable/

---------

Un finalizador de clase, es una método que se ejecuta cuando el objeto
es destruido, pero no por el usuario, si no por el GC.

En C# no existe el "destructor de clase".

.. warning::
    Ver IDisposable(abajo) para hacer este tipo de cosas

Mi problema fue con un código como el siguiente

.. code-block:: c#

    class Point
    {
        public Point()
        {
            Console.WriteLine(1);
        }

        ~Point()
        {
            Console.WriteLine(2);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Point p = new Point();
            p = null;
            Console.WriteLine(3);
        }
    }

Resultado

.. code-block:: bash

    1
    3
    2

En teoría, o según lo hace PHP, cuando se destruye un objeto
(obj = null), o cuando finaliza por que ya no se referencia mas,
el método __destruct() es llamado.

En C#, que se llama finalilzador, no hace lo mismo, al menos
no cuando se destruye de manera explicita asignándole 'null'.

Encontré en los comentarios un código, y al menos me hizo lo
que esperaba que hiciera, que lanzara el finalizador en cuanto
lo destruyera.

.. code-block:: c#

    Point p = new Point();
    p = null;
    GC.Collect();
    GC.WaitForPendingFinalizers();
    Console.WriteLine(3);

Ahora el resultado es

.. code-block:: bash

    1
    2
    3

Interfaz IDisposable (Recomendado)
**********************************

Otra manera, seria que la clase implemente la interfaz ``IDisposable``
con un único miembro ``Dispose``, dentro del método se podrían
añadir la limpieza necesaria de la clase.
