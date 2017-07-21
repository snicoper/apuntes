.. _reference-programacion-asp_mvc-validacion_modelos:

#####################
Validación de modelos
#####################

**Fuentes**

* https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation
* https://msdn.microsoft.com/library/system.componentmodel.dataannotations(v=vs.110).aspx

-----------

## Implementar IValidatableObject

* https://www.youtube.com/watch?v=fQRm0XlRCOo

.. code-block:: csharp

    public class Usuario : IValidatableObject
    {
        // ...
        public string Username { get; set; }

        public IEnumerable<ValidationResult> Validate(ValidationContext validationContext)
        {
            var errors = new List<ValidationResult>();

            // Comprobar si el nombre esta en la db.

            return errors;
        }
    }
