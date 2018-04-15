.. _reference-programacion-csharp-dotnet_core-acceder_desde_dispositivo_en_dev:

############################################
Acceder desde otro dispositivo en desarrollo
############################################

-----

Probado en **ASPNET Core 2.1**

A veces es util acceder desde una tablet o movil para ver como esta quedando la cosa.

Editar ``Program.cs`` el método ``CreateWebHostBuilder``

.. code-block:: csharp

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        return WebHost.CreateDefaultBuilder(args)
            .UseUrls(
                "http://192.168.1.107:50000", # Ip local
                "http://localhost:50000")
            .UseStartup<Startup>();
    }

Tener puertos abiertos.
