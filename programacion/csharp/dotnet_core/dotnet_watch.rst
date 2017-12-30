.. _reference-programacion-csharp-dotnet_core-index:

################
dotnet watch run
################

Editar ``NameProject.csproj``

.. code-block:: json

    <ItemGroup>
      <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.1" />

      <!-- Añadir -->
      <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>

.. code-block:: bash

    dotnet restore
    dotnet watch run
