.. _reference-programacion-csharp-dotnet_core-router_lowercase_and_slash:

##########################
Router lowercase and slash
##########################

Editar ``Startup.cs``

.. code-block:: csharp

    // This method gets called by the runtime. Use this method to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        services.AddRouting(options => {
            options.AppendTrailingSlash = true;
            options.LowercaseUrls = true;
        });
    }
