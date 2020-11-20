.. _reference-linux-dotnet-instalacion_fedora_centos:

########################################
Instalación dotnet core en Fedora/Centos
########################################

Fuentes

* https://docs.microsoft.com/es-es/dotnet/core/install/linux-fedora

----

Fedora >= 32
============

Repos de fedora

.. code-block:: bash

    sudo dnf install dotnet-sdk-3.1

Repos de microsoft

.. code-block:: bash

    sudo vim /etc/yum.repos.d/fedora.repo

    # Añadir
    exclude=dotnet* aspnetcore* netstandard*

.. code-block:: bash

    sudo vim /etc/yum.repos.d/fedora-updates.repo

    # Añadir
    exclude=dotnet* aspnetcore* netstandard*

.. code-block:: bash

    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/33/prod.repo

    sudo dnf install dotnet-sdk-2.1 dotnet-sdk-3.1 dotnet-sdk-5.0

Centos 8
========

.. code-block:: bash

    sudo dnf install dotnet-sdk-3.1

Centos 7
========

Añadir repos de **dotnet**

.. code-block:: bash

    sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm

Instalar **.NET SDK**

.. code-block:: bash

    sudo yum update
    sudo yum install dotnet-sdk-3.0

Creación app
============

.. code-block:: bash

    dotnet new -l

Muestra un listado de **Templates** para usar con ``dotnet new``

.. code-block:: bash

    Templates                                         Short Name       Language          Tags
    --------------------------------------------------------------------------------------------------------
    Console Application                               console          [C#], F#, VB      Common/Console
    Class library                                     classlib         [C#], F#, VB      Common/Library
    Unit Test Project                                 mstest           [C#], F#, VB      Test/MSTest
    xUnit Test Project                                xunit            [C#], F#, VB      Test/xUnit
    ASP.NET Core Empty                                web              [C#], F#          Web/Empty
    ASP.NET Core Web App (Model-View-Controller)      mvc              [C#], F#          Web/MVC
    ASP.NET Core Web App                              razor            [C#]              Web/MVC/Razor Pages
    ASP.NET Core with Angular                         angular          [C#]              Web/MVC/SPA
    ASP.NET Core with React.js                        react            [C#]              Web/MVC/SPA
    ASP.NET Core with React.js and Redux              reactredux       [C#]              Web/MVC/SPA
    ASP.NET Core Web API                              webapi           [C#], F#          Web/WebAPI
    global.json file                                  globaljson                         Config
    Nuget Config                                      nugetconfig                        Config
    Web Config                                        webconfig                          Config
    Solution File                                     sln                                Solution
    Razor Page                                        page                               Web/ASP.NET
    MVC ViewImports                                   viewimports                        Web/ASP.NET
    MVC ViewStart                                     viewstart                          Web/ASP.NET
