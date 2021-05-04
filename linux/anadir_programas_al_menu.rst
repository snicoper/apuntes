.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

Jetbrains toolbox local
***********************

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

Rider local
***********

.. code-block:: bash

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

Postman local
*************

.. code-block:: bash

    gzip -d Postman-linux-x64-8.0.1.tar.gz
    tar -xvf Postman-linux-x64-8.0.1.tar
    mv Postman ~/.apps/postman
    chmod +x ~/.apps/postman/Postman
    ln -s ~/.apps/postman/Postman ~/.bin/postman

.. code-block:: bash

    vim ~/.local/share/applications/postman.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Postman
    Comment=API Development
    Exec=postman %U
    Icon=/home/snicoper/.apps/postman/app/resources/app/assets/icon.png
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
