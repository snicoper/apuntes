.. _reference-linux-dotnet-instalacion_fedora_centos:

########################################
Instalación dotnet core en Fedora/Centos
########################################

Fuentes

* https://www.microsoft.com/net/learn/get-started/linuxredhat

----

Básicamente la instalación es la misma.

Fedora > 26
===========

Añadir repos de **dotnet**

.. code-block:: bash

    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'


Instalar **.NET SDK**

.. code-block:: bash

    dnf update
    dnf install libunwind libicu compat-openssl10
    dnf install dotnet-sdk-2.1.105-2.1.105-1.x86_64

    dotnet --info

.. note:: La ultima version probada de 2.1.4 en fedora 28 beta, ``dotnet xxx`` daba un problema ``error MSB1025: An internal failure occurred while running MSBuild.``, lo he solucionado añadiendo en ``.zshrc`` o ``.bashrc`` ``alias dotnet="TERM=xterm dotnet"`` https://github.com/dotnet/corefx/issues/26966

Centos 7
========

Añadir repos de **dotnet**

.. code-block:: bash

    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl= https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'

Instalar **.NET SDK**

.. code-block:: bash

    yum update
    yum install libunwind libicu
    yum install dotnet-sdk-2.1.105-2.1.105-1.x86_64

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
