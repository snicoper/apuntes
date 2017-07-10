.. _reference-programacion-asp_mvc-append_slash_router:

######################
Append slash en la URI
######################

Añade en las **URLs** el slash al final ``\``

Editar Editar ``App_Start/RouteConfig.cs`` y añadir ``routes.AppendTrailingSlash = true;``

.. code-block:: csharp

    public class RouteConfig
    {
        public static void RegisterRoutes(RouteCollection routes)
        {
            routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

            routes.AppendTrailingSlash = true;

            routes.MapRoute(
                name: "Default",
                url: "{controller}/{action}/{id}",
                defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
            );
        }
    }