.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

Rider local
***********

.. code-block:: bash

    su -
    gzip -d JetBrains.Rider-2018.1.tar.gz
    tar -xvf JetBrains.Rider-2018.1.tar
    mv JetBrains\ Rider-2018.1 ~/.apps/rider
    chmod +x ~/.apps/rider/bin/rider.sh
    ln -s ~/.apps/rider/bin/rider.sh ~/.bin/rider

.. code-block:: bash

    vim ~/.local/share/applications/rider.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Rider
    Comment=IDE for DotNet Core
    Exec=rider %U
    Icon=/home/snicoper/.apps/rider/bin/rider.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

SmartGit local
**************

.. code-block:: bash

    su -
    gzip -d smartgit-linux-18_2_3.tar.gz
    tar -xvf smartgit-linux-18_2_3.tar
    mv smartgit ~/.apps/smartgit
    chmod +x ~/.apps/smartgit/bin/smartgit.sh
    ln -s ~/.apps/smartgit/bin/smartgit.sh ~/.bin/smartgit

.. code-block:: bash

    vim ~/.local/share/applications/smartgit.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=SmartGit
    Comment=Graphical Git client
    Exec=smartgit %U
    Icon=/home/snicoper/.apps/smartgit/bin/smartgit-32.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

PyCharm
*******

.. code-block:: bash

    su -
    gzip -d pycharm-professional-2018.3.tar.gz
    tar -xvf pycharm-professional-2018.3.tar
    mv pycharm-2018.3/ /opt/pycharm
    chmod +x /opt/pycharm/bin/pycharm.sh
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

WebStorm
********

.. code-block:: bash

    su -
    gzip -d WebStorm-2018.1.2.tar.gz
    tar -xvf WebStorm-2018.1.2.tar
    mv WebStorm-2018.1.2 /opt/webstorm
    chmod +x /opt/webstorm/bin/webstorm.sh
    ln -s /opt/webstorm/bin/webstorm.sh /usr/local/bin/webstorm

.. code-block:: bash

    vim /usr/share/applications/webstorm.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=WebStorm
    Comment=IDE for Web
    Exec=webstorm %U
    Icon=/opt/webstorm/bin/webstorm.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

DataGrip
********

.. code-block:: bash

    su -
    gzip -d datagrip-2018.2.4.tar.gz
    tar -xvf datagrip-2018.2.4.tar
    mv DataGrip-2018.2.4 /opt/datagrip
    chmod +x /opt/datagrip/bin/datagrip.sh
    ln -s /opt/datagrip/bin/datagrip.sh /usr/local/bin/datagrip

.. code-block:: bash

    vim /usr/share/applications/datagrip.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=DataGrip
    Comment=Database tools
    Exec=datagrip %U
    Icon=/opt/datagrip/bin/datagrip.png
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

SmartGit
********

.. code-block:: bash

    su -
    gzip -d smartgit-linux-18_2_3.tar.gz
    tar -xvf smartgit-linux-18_2_3.tar
    mv smartgit /opt/smartgit
    chmod +x /opt/smartgit/bin/smartgit.sh
    ln -s /opt/smartgit/bin/smartgit.sh /usr/local/bin/smartgit

.. code-block:: bash

    vim /usr/share/applications/smartgit.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=SmartGit
    Comment=Graphical Git client
    Exec=smartgit %U
    Icon=/opt/smartgit/bin/smartgit-32.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true

Postman
*******

.. code-block:: bash

    su -
    gzip -d Postman-linux-x64-6.4.4.tar.gz
    tar -xvf Postman-linux-x64-6.4.4.tar
    mv Postman/ /opt/postman
    chmod +x /opt/postman/Postman
    ln -s /opt/postman/Postman /usr/local/bin/postman

.. code-block:: bash

    vim /usr/share/applications/postman.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Postman
    Comment=Postman
    Exec=postman %U
    Icon=/opt/postman/app/resources/app/assets/icon.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true
