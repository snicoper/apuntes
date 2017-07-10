.. _reference-programacion-asp_mvc-lower_case_route_asp_net_mvc:

# Route ASP.net MVC lowercase

Editar `App_Start/RouteConfig.cs`

.. code-block:: csharp

    public class RouteConfig
    {
        public static void RegisterRoutes(RouteCollection routes)
        {
            routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

            routes.LowercaseUrls = true;

            routes.MapRoute(
                name: "Default",
                url: "{controller}/{action}/{id}",
                defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
            );
        }
    }