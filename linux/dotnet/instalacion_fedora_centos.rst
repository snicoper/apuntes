.. _reference-linux-dotnet-instalacion_fedora_centos:

########################################
Instalación dotnet core en Fedora/Centos
########################################

Fuentes

* https://docs.microsoft.com/es-es/dotnet/core/install/linux-fedora

----

Fedora 40
=========

.. code-block:: bash

    sudo dnf install dotnet-sdk-8.0

Versiones next
==============

Instalar `dotnet 8.0.100-rc`

* https://github.com/dotnet/core/blob/main/release-notes/8.0/install-linux.md#installing-from-a-binary-archive

Editar `.zshrc` o `.bashrc``

.. code-block:: bash

    export DOTNET_ROOT=~/.dotnet
    export PATH=$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools
    export PATH=$PATH:~/.dotnet

    curl -Lo dotnet.tar.gz https://download.visualstudio.microsoft.com/download/pr/8cccb582-1956-422a-8655-fad2fa12c247/4e86a676860c2ced06228a5c8d21718d/dotnet-sdk-8.0.100-rc.1.23455.8-linux-x64.tar.gz
    mkdir ~/dotnet
    tar -C ~/.dotnet -xf dotnet.tar.gz
    rm dotnet.tar.gz
    dotnet --version

.. code-block:: bash

    ./dotnet-install.sh --runtime dotnet --channel 8.0 --quality preview --install-dir ~/.bin/dotnet-cli

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
