.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

.. note::
    Si da problemas de permisos, ver https://askubuntu.com/a/169317

PyCharm
*******

.. code-block:: bash

    su -
    gzip -d pycharm-professional-2018.1.1.tar.gz
    tar -xvf pycharm-professional-2018.1.1.tar
    mv pycharm-2018.1.1/ /opt/pycharm
    chmod +x /opt/pycharm/bin/pycharm.sh

.. code-block:: bash

    ln -s /opt/pycharm/bin/pycharm.sh /usr/local/bin/pycharm

.. code-block:: bash

    vim /usr/share/applications/pycharm.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=PyCharm
    Comment=IDE for Python
    Exec=pycharm %U
    Icon=/opt/pycharm/bin/pycharm.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

Rider
*****

.. code-block:: bash

    su -
    gzip -d JetBrains.Rider-2018.1.tar.gz
    tar -xvf JetBrains.Rider-2018.1.tar
    mv JetBrains\ Rider-2018.1 /opt/rider
    chmod +x /opt/rider/bin/rider.sh

.. code-block:: bash

    ln -s /opt/rider/bin/rider.sh /usr/local/bin/rider

.. code-block:: bash

    vim /usr/share/applications/rider.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Rider
    Comment=IDE for DotNet Core
    Exec=rider %U
    Icon=/opt/rider/bin/rider.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

Discord
*******

.. code-block:: bash

    sudo dnf install libXScrnSaver

De momento esta en una fase muy temprana

Descargar y descomprimir de `GitHub <https://github.com/crmarsh/discord-linux-bugs>`_

.. code-block:: bash

    su -
    mv DiscordCanary /opt/discord
    chmod +x /opt/discord/DiscordCanary

.. code-block:: bash

    ln -s /opt/discord/DiscordCanary /usr/local/bin/discord

.. code-block:: bash

    vim /usr/share/applications/discord.desktop

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

Dbeaver
*******

.. code-block:: bash

    su -
    gzip -d dbeaver-ce-5.0.3-linux.gtk.x86_64.tar.gz
    tar -xvf dbeaver-ce-5.0.3-linux.gtk.x86_64.tar
    mv dbeaver /opt/dbeaver
    chmod +x /opt/dbeaver/dbeaver

.. code-block:: bash

    ln -s /opt/dbeaver/dbeaver /usr/local/bin/dbeaver

.. code-block:: bash

    vim /usr/share/applications/dbeaver.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Dbeaver
    Comment=Universal SQL Client
    Exec=dbeaver %U
    Icon=/opt/dbeaver/icon.xpm
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true
