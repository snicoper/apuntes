.. _reference-programacion-csharp-checked_unchecked:

#################
Checked Unchecked
#################

Sirve para comprobar el desbordamiento, con ``checked`` lo comprueba,
``unchecked`` no lo hace.

Por ejemplo

.. code-block:: c#

    byte a = 55;
    byte b = 210;
    byte result = (byte)(a + b);

El comportamiento por defecto, depende de la configuración de compilación, pero
creo que es ``unchecked``.

.. code-block:: c#

    unchecked
    {
        byte a = 55;
        byte b = 210;
        byte result = (byte)(a + b);
    }

El ejemplo anterior, dará como resultado 9, ya que un byte solo puede contener un
entero entre 0 y 255.

La suma es de 210 + 55 = 265 (supera en 10 al máximo), por lo que que cuando llega a
255 el siguiente numero es 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 que son los 10 extras.

Con checked

.. code-block:: c#

    checked
    {
        byte a = 55;
        byte b = 210;
        byte result = (byte)(a + b);
    }

Lanzara una ``System.OverflowException``

Conclusión, si es importante que no sobrepase el máximo de un tipo, usar ``checked``
