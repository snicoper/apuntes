.. _reference-programacion-csharp-boxing_unbonxing:

##################
Boxing y Unbonxing
##################

Fuentes
*******

* http://msdn.microsoft.com/es-es/library/yz2be5wk.aspx

--------

Boxing se refiere a la conversión de un tipo valor a un tipo object ajustable.

Unboxing es lo contrario, un tipo objeto a un tipo valor
(siempre que sea posible), además se debe hacer de manera explícita.

Boxing
******

.. code-block:: c#

    int i = 1;
    object o = i;

Unbonxing
*********

.. code-block:: c#

    int e = (int)o;

La utilidad viene mas cuando se usan por ejemplo, listas

.. code-block:: c#

    using System.Collections;
    [……]

    ArrayList array = new ArrayList();
    array.Add(12);
    array.Add(3);
    array.Add(123);

Si ahora queremos obtener los valores y asignarlos a variables, como
ArrayList no sabe los tipos de sus valores, debemos hacer Unboxing
de manera explicita:

.. code-block:: c#

    int num = (int)array[1];

.. note::
    Aun asi, si necesitamos listas de un tipo concreto, usar
    ``System.Collections.Generic``
