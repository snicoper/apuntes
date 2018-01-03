.. _reference-programacion-csharp-dotnet_core-create_template_dotnet_core:

#############################
Crear template de un proyecto
#############################

POR HACER...

.. code-block:: json

    {
      "author": "Salvador Nicolas",
      "classifications": [ "Web", "MVC" ],
      "name": "Template test",
      "identity": "templatetest",
      "shortName": "teplatetest",
      "tags": {
        "language": "C#"
      },
      "sourceName": "PartyInvites",
      "preferNameDirectory" : "true"
    }

.. code-block:: bash

    dotnet new -i "/home/snicoper/Desktop/PartyInvites"
    dotnet new -u "/home/snicoper/Desktop/PartyInvites"
    dotnet new teplatetest -n Contoso.Web -o Contoso.Web
