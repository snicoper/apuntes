.. _reference-programacion-csharp-fields_and_properties:

####################
Campos y Propiedades
####################

Un campo es el equivalente de una propiedad en PHP.

.. code-block:: c#

    private string nombre;

Una propiedad es un setters/getter con posible lógica sobre un campo.

.. code-block:: c#

    public string Nombre
    {
        set
        {
            if (value.Length < 5)
            {
                // hacer algo
            }
            else
            {
                nombre = value;
            }
        }
        get { return nombre; }
    }

A groso modo, se puede decir que un campo(field) son como las propiedades en PHP
y las propiedades son los métodos accesores en PHP.

Internamente cuando lo convierte a ¿``CIL``?, crea métodos accesores como en PHP, es un
atajo para el desarrollador.
