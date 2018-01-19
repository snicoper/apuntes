.. _reference-programacion-csharp-dotnet_core-manage_global_exceptions:

############################
Manejar excepciones globales
############################

**Fuentes**

* http://www.talkingdotnet.com/global-exception-handling-in-aspnet-core-webapi/

------

Crear un filtro ``ExceptionHandlingFilter``

.. code-block:: csharp

    public class ExceptionHandlingFilter : IExceptionFilter
    {
        public void OnException(ExceptionContext context)
        {
            var exception = context.Exception;
            var path = context.HttpContext.Request.Path;

            // Manejar la exception
        }
    }

Añadir el filtro en el método ``ConfigureServices`` de la clase ``Startup``

.. code-block:: csharp

    services.AddMvc().AddMvcOptions(options =>
    {
        options.Filters.Add(typeof(ExceptionHandlingFilter));
    });
