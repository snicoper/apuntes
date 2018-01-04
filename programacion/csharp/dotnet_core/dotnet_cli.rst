.. _reference-programacion-csharp-dotnet_core-dotnet_cli:

##########
DotNet CLI
##########

**Fuentes**

* https://docs.microsoft.com/en-us/dotnet/core/tools/?tabs=netcore2x

-----

Help
====

.. code-block:: bash

    dotnet -h # dotnet -h
    dotnet command -h # dotnet new -h
    dotnet command command -h # dotnet new sln -h

Creación de una solución
========================

.. code-block:: bash

    dotnet new sln -n NombreSolution -o NombreSolution && cd NombreSolution

Creación proyectos
==================

.. code-block:: bash

    dotnet new web -n NombreSolution.Web -o NombreSolution.Web
    dotnet new classlib -n NombreSolution.Domain -o NombreSolution.Domain
    dotnet new xunit -n NombreSolution.Tests -o NombreSolution.Tests

Añadir/quitar proyectos a una solución
======================================

Añadir de uno en uno a una solución.

.. code-block:: bash

    dotnet sln add NombreSolution.sln NombreSolution.Web/NombreSolution.Web.csproj
    dotnet sln add NombreSolution.sln NombreSolution.Domain/NombreSolution.Domain.csproj
    dotnet sln add NombreSolution.sln NombreSolution.Tests/NombreSolution.Tests.csproj

Eliminar de uno en uno en una solución

.. code-block:: bash

    dotnet sln remove NombreSolution.sln NombreSolution.Web/NombreSolution.Web.csproj
    dotnet sln remove NombreSolution.sln NombreSolution.Domain/NombreSolution.Domain.csproj
    dotnet sln remove NombreSolution.sln NombreSolution.Tests/NombreSolution.Tests.csproj

Añadir varios proyectos a una solución

.. code-block:: bash

    dotnet sln add NombreSolution.sln  **/*.csproj

Quitar varios proyectos a una solución

.. code-block:: bash

    dotnet sln remove NombreSolution.sln  **/*.csproj

Referenciar proyectos
=====================

Referenciar un proyecto con otro.

``Web`` -> ``Domain``
``Tests`` -> ``Web`` -> ``Domain``

.. code-block:: bash

    dotnet add NombreSolution.Web/NombreSolution.Web.csproj reference NombreSolution.Domain/NombreSolution.Domain.csproj
    dotnet add NombreSolution.Tests/NombreSolution.Tests.csproj reference NombreSolution.Web/NombreSolution.Web.csproj
    dotnet add NombreSolution.Tests/NombreSolution.Tests.csproj reference NombreSolution.Domain/NombreSolution.Domain.csproj

Eliminar referencia

.. code-block:: bash

    dotnet remove NombreSolution.Web/NombreSolution.Web.csproj reference NombreSolution.Domain/NombreSolution.Domain.csproj
    dotnet remove NombreSolution.Tests/NombreSolution.Tests.csproj reference NombreSolution.Web/NombreSolution.Web.csproj
    dotnet remove NombreSolution.Tests/NombreSolution.Tests.csproj reference NombreSolution.Domain/NombreSolution.Domain.csproj

Instalar/desinstalar packages
=============================

Si se esta dentro del proyecto se omitir NombreSolution.XXX.csproj

Instalar packages

.. code-block:: bash

    dotnet add NombreSolution.Domain/NombreSolution.Domain.csproj package Microsoft.EntityFrameworkCore.Tools
    dotnet add NombreSolution.Domain/NombreSolution.Domain.csproj package Microsoft.EntityFrameworkCore.Design
    dotnet add NombreSolution.Domain/NombreSolution.Domain.csproj package Npgsql.EntityFrameworkCore.PostgreSQL

    # Dentro de NombreSolution.Domain
    # cd NombreSolution.Domain
    dotnet add package Microsoft.EntityFrameworkCore.Tools
    dotnet add package Microsoft.EntityFrameworkCore.Design
    dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL

Eliminar packages

.. code-block:: bash

    dotnet remove NombreSolution.Domain/NombreSolution.Domain.csproj package Microsoft.EntityFrameworkCore.Tools
    dotnet remove NombreSolution.Domain/NombreSolution.Domain.csproj package Microsoft.EntityFrameworkCore.Design
    dotnet remove NombreSolution.Domain/NombreSolution.Domain.csproj package Npgsql.EntityFrameworkCore.PostgreSQL

    # Dentro de NombreSolution.Domain
    # cd NombreSolution.Domain
    dotnet remove package Microsoft.EntityFrameworkCore.Tools
    dotnet remove package Microsoft.EntityFrameworkCore.Design
    dotnet remove package Npgsql.EntityFrameworkCore.PostgreSQL
