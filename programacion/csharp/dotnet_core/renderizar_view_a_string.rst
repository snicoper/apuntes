.. _reference-programacion-csharp-dotnet_core-renderizar_view_a_string:

############################
Renderizar una View a String
############################

**Fuentes**

* https://ppolyzos.com/2016/09/09/asp-net-core-render-view-to-string/

----

Para envió de emails.

Crear un **Servicio**

.. code-block:: csharp

    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.AspNetCore.Mvc.Abstractions;
    using Microsoft.AspNetCore.Mvc.ModelBinding;
    using Microsoft.AspNetCore.Mvc.Razor;
    using Microsoft.AspNetCore.Mvc.Rendering;
    using Microsoft.AspNetCore.Mvc.ViewFeatures;
    using Microsoft.AspNetCore.Routing;
    using System;
    using System.IO;
    using System.Threading.Tasks;

    namespace Prueba.Services
    {
        public interface IViewRenderService
        {
            Task<string> RederToStringAsync<TModel>(string viewName, TModel model);
        }

        public class ViewRenderService : IViewRenderService
        {
            private readonly IRazorViewEngine _razorViewEngine;
            private readonly ITempDataProvider _tempDataProvider;
            private readonly IServiceProvider _serviceProvider;

            public ViewRenderService(
                IRazorViewEngine razorViewEngine,
                ITempDataProvider tempDataDictionary,
                IServiceProvider serviceProvider)
            {
                _razorViewEngine = razorViewEngine;
                _tempDataProvider = tempDataDictionary;
                _serviceProvider = serviceProvider;
            }

            public async Task<string> RederToStringAsync<TModel>(string viewName, TModel model)
            {
                var httpContext = new DefaultHttpContext { RequestServices = _serviceProvider };
                var actionContext = new ActionContext(httpContext, new RouteData(), new ActionDescriptor());

                using (var sw = new StringWriter())
                {
                    var viewResult = _razorViewEngine.FindView(actionContext, viewName, false);

                    if (viewResult.View is null)
                    {
                        throw new ArgumentNullException($"{viewName} does not math any available view");
                    }

                    var viewDictionary = new ViewDataDictionary(
                        new EmptyModelMetadataProvider(),
                        new ModelStateDictionary()
                    )
                    {
                        Model = model
                    };

                    var viewContext = new ViewContext(
                        actionContext,
                        viewResult.View,
                        viewDictionary,
                        new TempDataDictionary(actionContext.HttpContext, _tempDataProvider),
                        sw,
                        new HtmlHelperOptions()
                    );

                    await viewResult.View.RenderAsync(viewContext);
                    return sw.ToString();
                }
            }
        }
    }

Registrar el Servicio

.. code-block:: csharp

    public void ConfigureServices(IServiceCollection services)
    {
        # ...
        services.AddScoped<IViewRenderService, ViewRenderService>();
    }
