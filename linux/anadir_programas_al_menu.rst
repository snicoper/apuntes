.. _reference-linux-anadir_programas_al_menu:

########################
Añadir programas al menu
########################

Jetbrains toolbox
*****************

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

Rider
*****

.. code-block:: bash

    gzip -d JetBrains.Rider-2023.2.2.tar.gz
    tar -xvf JetBrains.Rider-2023.2.2.tar
    mv mv JetBrains\ Rider-2023.2.2 ~/.apps/rider
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

SmartGit
********

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

Postman
*******

.. code-block:: bash

    gzip -d Postman-linux-x64-8.0.1.tar.gz
    tar -xvf Postman-linux-x64-8.0.1.tar
    mv Postman ~/.apps/postman
    chmod +x ~/.apps/postman/app/Postman
    ln -s ~/.apps/postman/app/Postman ~/.bin/postman

.. code-block:: bash

    vim ~/.local/share/applications/postman.desktop

.. code-block:: bash

    [Desktop Entry]
    Encoding=UTF-8
    Name=Postman
    Comment=API Development
    Exec=postman %U
    Icon=~/.apps/postman/app/icons/icon_128x128.png
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true
