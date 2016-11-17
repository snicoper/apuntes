.. _reference-programacion-csharp-csharp_script-platilla_crear_excepciones:

################################
Crear Excepciones personalizadas
################################

.. code-block:: c#

    public class CountIsZeroException : Exception
    {
        public CountIsZeroException()
        {
        }

        public CountIsZeroException(string message)
            : base(message)
        {
        }

        public CountIsZeroException(string message, Exception innerException)
            : base(message, innerException)
        {
        }
    }
