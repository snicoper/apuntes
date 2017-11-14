.. _reference-linux-instalacion_discord:

###################
Instalación Discord
###################

De momento no hay una versión final, pero si quieres estar hablando con tus colegas, quizá te pueda servir.

Todo se hace como súper usuario (su)

Requisitos
**********

.. code-block:: bash

    dnf install libXScrnSaver

Instalación
***********

Descargar de `GitHub <https://github.com/crmarsh/discord-linux-bugs>`_ el ``.tar.gz`` y descomprimir,
por ultimo ir al path donde este el descomprimido y como súper usuario:


.. code-block:: bash

    mv DiscordCanary /opt/discord
    chmod +x /opt/discord/DiscordCanary
    ln -s /opt/discord/DiscordCanary /usr/local/bin/discord

Por ultimo, crear un enlace al menú.

.. code-block:: bash

    vim /usr/share/applications/discord.desktop

Añadimos:

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Discord
    Comment=Chat
    Exec=discord %U
    Icon=/opt/discord/discord.png
    Terminal=false
    Type=Application
    StartupNotify=true
