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

Editar ``CustomerCenter.csproj``

.. code-block:: xml

    <Project Sdk="Microsoft.NET.Sdk.Web">
      <PropertyGroup>
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>

      <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.3" />

        <!-- Añadir -->
        <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="2.0.0" />
        <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="2.0.1" />
        <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="2.0.1" />
      </ItemGroup>

      <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.1" />

        <!-- Añadir -->
        <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
      </ItemGroup>
    </Project>

.. code-block:: bash

    dotnet restore

ApplicationDbContext
====================

Crear ``ApplicationDbContext.cs`` dentro del directorio ``Models``

.. code-block:: csharp

    using Microsoft.EntityFrameworkCore;

    namespace MySite.Models
    {
        class ApplicationDbContext : DbContext
        {
            public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) {}
        }
    }

Startup.cs
==========

Editar el método ``ConfigureServices``

.. code-block:: csharp

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        services.AddEntityFrameworkNpgsql().AddDbContext<ApplicationDbContext>(opt =>
                opt.UseNpgsql(Configuration.GetConnectionString("ApplicationDbContext"))
        );
    }

appsettings
===========

Editar ``appsettings.Development.json``, añadiendo ``ConnectionString``

.. code-block:: json

    {
      "ConnectionStrings": {
        "ApplicationDbContext": "User Id=snicoper;Password=123456;Server=localhost;Port=5432;Database=practicas;Integrated Security=true;Pooling=true;"
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

    namespace CustomerCenter.Models
    {
        public class Persona
        {
            public int Id { get; set; }
            public string Name { get; set; }
        }
    }

Editar ``Models/ApplicationDbContext.cs`` y añadir la propiedad:

.. code-block:: csharp

    public DbSet<Persona> Personas { get; set; }

Añadir migración y actualizad la base de datos
==============================================

.. code-block:: bash

    dotnet ef migrations add Initial
    dotnet ef database update
