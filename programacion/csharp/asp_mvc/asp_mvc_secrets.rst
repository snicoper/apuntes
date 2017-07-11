.. _reference-programacion-asp_mvc-asp_mvc_secrets:

##################################
Archivo configuración para secrets
##################################

Editar ``Web.config`` y añadir ``file="secrets.config"`` en ``<appSettings>``

.. code-block:: xml

    <appSettings file="secrets.config">
        <add key="webpages:Version" value="3.0.0.0"/>
        <add key="webpages:Enabled" value="false"/>
        <add key="ClientValidationEnabled" value="true"/>
        <add key="UnobtrusiveJavaScriptEnabled" value="true"/>
    </appSettings>

Crear en la raiz (donde Web.config) ``secrets.config`` y añadir lo parametros.

.. code-block:: xml

    <appSettings>
        <add key="Host" value=""/>
        <add key="EnableSsl" value=""/>
        <add key="UserName" value=""/>
        <add key="Password" value=""/>
        <add key="Port" value="" />
    </appSettings>

Por ultimo, añadirlo a ``.gitignore``

.. code-block:: txt

    secrets.config