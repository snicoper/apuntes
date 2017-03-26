.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

.. note::
    Todos los pongo en ``/opt``

    Prácticamente todos son iguales, solo cambian las rutas, pero las pongo separadas
    para ir mas rápido si algún día tengo que instalar alguno.

Sublime 3
*********

Descomprimir como usuario

.. code-block:: bash

    su -
    mv sublime_text_3 /opt/sublime_text_3
    chmod +x /opt/sublime_text_3/sublime_text

.. code-block:: bash

    ln -s /opt/sublime_text_3/sublime_text /usr/local/bin/subl

.. code-block:: bash

    vim /usr/share/applications/sublime.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Sublime Text 3
    Comment=Sublime Text Editor
    Exec=subl %U
    # Icon=/home/snicoper/.local/share/icons/Paper/48x48/apps/sublime-text.png
    Icon=/opt/sublime_text_3/Icon/48x48/sublime-text.png
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
    gzip -d pycharm-professional-2017.1.tar.gz
    tar -xvf pycharm-professional-2017.1.tar
    mv pycharm-2017.1/ /opt/jetbrains/pycharm
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

Telegram
********

Para mostrar icono en la bandeja

.. code-block:: bash

    dnf install libappindicator-gtk3

    # Alt+F2 -> r (Enter)

.. code-block:: bash

    su -
    tar Jxvf tsetup.0.9.40.tar.xz
    chmod +x Telegram/Telegram
    mv Telegram /opt/Telegram

.. code-block:: bash

    ln -s /opt/Telegram/Telegram /usr/local/bin/telegram

.. code-block:: bash

    vim /usr/share/applications/telegram.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Telegram
    Comment=Chat
    Exec=telegram %U
    Icon=/home/snicoper/.local/share/icons/telegram.png
    Terminal=false
    Type=Application
    StartupNotify=true
