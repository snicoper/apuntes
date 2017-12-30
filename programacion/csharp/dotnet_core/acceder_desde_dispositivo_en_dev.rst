.. _reference-programacion-csharp-dotnet_core-acceder_desde_dispositivo_en_dev:

############################################
Acceder desde otro dispositivo en desarrollo
############################################

**Fuentes**

* https://stackoverflow.com/a/37365198

-----

A veces es util acceder desde una tablet o movil para ver como esta quedando la cosa.

Editar ``Program.cs`` el método ``Main``

.. code-block:: csharp

    public static void Main(string[] args)
    {
        // use this to allow command line parameters in the config
        var configuration = new ConfigurationBuilder()
            .AddCommandLine(args)
            .Build();

        var hostUrl = configuration["hosturl"];
        if (string.IsNullOrEmpty(hostUrl))
        {
            hostUrl = "http://0.0.0.0:5000";
        }

        var host = new WebHostBuilder()
            .UseKestrel()
            .UseUrls(hostUrl)
            .UseContentRoot(Directory.GetCurrentDirectory())
            .UseIISIntegration()
            .UseStartup<Startup>()
            .UseConfiguration(configuration)
            .Build();

        host.Run();
    }

.. code-block:: bash

    dotnet run                                       // default on port 5000
    dotnet run --hosturl http://192.168.1.101:5000   // explicit

Tener puertos abiertos.
