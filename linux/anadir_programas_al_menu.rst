.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

.. note::
    Todos los pongo en ``/opt``

    Prácticamente todos son iguales, solo cambian las rutas, pero las pongo separadas
    para ir mas rápido si algún día tengo que instalar alguno.

PyCharm
*******

.. code-block:: bash

    su -
    # Si no existe /opt/jetbrains
    mkdir /opt/jetbrains
    gzip -d pycharm-professional-2017.3.2.tar.gz
    tar -xvf pycharm-professional-2017.3.2.tar
    mv pycharm-2017.3.2/ /opt/jetbrains/pycharm
    chmod +x /opt/jetbrains/pycharm/bin/pycharm.sh

.. code-block:: bash

    ln -s /opt/jetbrains/pycharm/bin/pycharm.sh /usr/local/bin/pycharm

.. code-block:: bash

    vim /usr/share/applications/pycharm.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=PyCharm
    Comment=IDE for Python
    Exec=pycharm %U
    Icon=/opt/jetbrains/pycharm/bin/pycharm.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

PyCharm
*******

.. code-block:: bash

    su -
    # Si no existe /opt/jetbrains
    mkdir /opt/jetbrains
    gzip -d JetBrains.Rider-2018.1-EAP8-181.4379.974.Checked.tar.gz
    tar -xvf JetBrains.Rider-2018.1-EAP8-181.4379.974.Checked.tar
    mv JetBrains\ Rider-181.4379.974 /opt/jetbrains/rider
    chmod +x /opt/jetbrains/rider/bin/rider.sh

.. code-block:: bash

    ln -s /opt/jetbrains/rider/bin/rider.sh /usr/local/bin/rider

.. code-block:: bash

    vim /usr/share/applications/rider.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Rider
    Comment=IDE for DotNet Core
    Exec=rider %U
    Icon=/opt/jetbrains/rider/bin/rider.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

WebStrom
********

.. code-block:: bash

    su -
    # Si no existe /opt/jetbrains
    mkdir /opt/jetbrains
    gzip -d WebStorm-11.0.1.tar.gz
    tar -xvf WebStorm-11.0.1.tar
    mv WebStorm-143.382.36/ /opt/jetbrains/webstorm
    chmod +x /opt/jetbrains/webstorm/bin/webstorm.sh

.. code-block:: bash

    ln -s /opt/jetbrains/webstorm/bin/webstorm.sh /usr/local/bin/webstorm

.. code-block:: bash

    vim /usr/share/applications/webstorm.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=webstorm
    Comment=IDE for Web
    Exec=webstorm %U
    Icon=/opt/jetbrains/webstorm/bin/webstorm.svg
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

Rider
*****

.. code-block:: bash

    su -
    # Si no existe /opt/jetbrains
    mkdir /opt/jetbrains
    gzip -d JetBrains.Rider-2017.3.tar.gz
    tar -xvf JetBrains.Rider-2017.3.tar
    mv JetBrains\ Rider-2017.3/ /opt/jetbrains/rider
    chmod +x /opt/jetbrains/rider/bin/rider.sh

.. code-block:: bash

    ln -s /opt/jetbrains/rider/bin/rider.sh /usr/local/bin/rider

.. code-block:: bash

    vim /usr/share/applications/rider.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Rider
    Comment=IDE for Web
    Exec=rider %U
    Icon=/opt/jetbrains/rider/bin/rider.png
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
    gzip -d dbeaver-ce-4.3.2-linux.gtk.x86_64.tar.gz
    tar -xvf dbeaver-ce-4.3.2-linux.gtk.x86_64.tar
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

Eclipse
*******

.. code-block:: bash

    su -
    gzip -d eclipse-javascript-oxygen-2-linux-gtk-x86_64.tar.gz
    tar -xvf eclipse-javascript-oxygen-2-linux-gtk-x86_64.tar
    mv eclipse /opt/eclipse
    chmod +x /opt/eclipse/eclipse

.. code-block:: bash

    ln -s /opt/eclipse/eclipse /usr/local/bin/eclipse

.. code-block:: bash

    vim /usr/share/applications/eclipse.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Eclipse
    Comment=Ide
    Exec=eclipse %U
    Icon=/opt/eclipse/icon.xpm
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true
