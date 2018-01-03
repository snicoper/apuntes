.. _reference-programacion-csharp-dotnet_core-dotnet_core_postgresql:

###############################
Añadir PostgreSQL a DotNet Core
###############################

Creación del proyecto
=====================

.. code-block:: bash

    mkdir MySite
    cd MySite

    dotnet new mvc

Packages
========

.. code-block:: bash

    dotnet add package Microsoft.EntityFrameworkCore.Tools
    dotnet add package Microsoft.EntityFrameworkCore.Design
    dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL

Editar ``MySite.csproj``

.. code-block:: xml

    <Project Sdk="Microsoft.NET.Sdk.Web">
      <!-- #... -->
      <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.1" />

        <!-- Añadir -->
        <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
      </ItemGroup>
    </Project>

.. code-block:: bash

    dotnet restore

AppDbContext
====================

Crear ``AppDbContext.cs`` dentro del directorio ``Models``

.. code-block:: csharp

    using Microsoft.EntityFrameworkCore;

    namespace MySite.Models
    {
        public class AppDbContext : DbContext
        {
            public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) {}
        }
    }

Startup.cs
==========

Editar el método ``ConfigureServices``

.. code-block:: csharp

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        services.AddEntityFrameworkNpgsql().AddDbContext<AppDbContext>(opt =>
            opt.UseNpgsql(Configuration.GetConnectionString("AppDbContext"))
        );
    }

appsettings
===========

Editar ``appsettings.Development.json``, añadiendo ``ConnectionString``

.. code-block:: json

    {
      "ConnectionStrings": {
        "AppDbContext": "User Id=snicoper;Password=123456;Server=localhost;Port=5432;Database=practicas;Integrated Security=true;Pooling=true;"
      },
      "Logging": {
        "IncludeScopes": false,
        "LogLevel": {
        "Default": "Debug",
        "System": "Information",
        "Microsoft": "Information"
        }
      }
    }

Probar
======

Dentro de ``Models`` crear ``Persona.cs`` con el siguiente código.

.. code-block:: csharp

    namespace MySite.Models
    {
        public class Persona
        {
            public int Id { get; set; }
            public string Name { get; set; }
        }
    }

Editar ``Models/AppDbContext.cs`` y añadir la propiedad:

.. code-block:: csharp

    public DbSet<Persona> Personas { get; set; }

Añadir migración y actualizad la base de datos
==============================================

.. code-block:: bash

    dotnet ef migrations add Initial
    dotnet ef database update
