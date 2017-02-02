.. _reference-programacion-csharp-metodos_extension_csharp:

#######################
Métodos de Extensión C#
#######################

Fuentes
*******

* http://msdn.microsoft.com/es-es/library/bb383977.aspx

---------

Cita de MSDN

.. raw:: html

    <cite>
        Los métodos de extensión permiten "agregar" métodos a los tipos existentes
        sin crear un nuevo tipo derivado, recompilar o modificar de otra manera el
        tipo original. Los métodos de extensión son una clase especial de método
        estático, pero se les llama como si fueran métodos de instancia en el tipo
        extendido. En el caso del código de cliente escrito en C# y Visual Basic,
        no existe ninguna diferencia aparente entre llamar a un método de extensión
        y llamar a los métodos realmente definidos en un tipo.
    </cite>

Ejemplo simple
**************

Los métodos de extensión deben estar en una clase ``static`` y el método también
ha de ser ``static``.

.. code-block:: c#

    public static clss StringExtension
    {
        public static string UcFirst(this string str)
        {
            if (str.Length == 0)
            {
                return string.Empty;
            }

            return string.Format("{0}{1}", str[0].ToUpper(), str.SubString(1));
        }
    }

El primer parámetro ``UcFirst(this string str)`` con ``this`` le decimos
a que hace referencia, en este caso es un tipo ``string``, pero podría
ser cualquier tipo.

Después del primer parámetro, se pueden poner tantos como se quiera,
lo que al llamar al método, el "primer" argumento se omite.

.. code-block:: c#

    string nombre = "salvador";

    Console.WriteLine(nombre.UcFirst()); // Salvador

Al ser una extensión de ``string`` al ``nombre.MyExtension()`` es como si
el método fuera parte del string.
