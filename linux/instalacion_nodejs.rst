.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

.. code-block:: bash

    sudo dnf -y install nodejs
    sudo dnf -y install npm

Si después se actualiza **npm** con ``sudo npm install npm -g`` a la hora de actualizar el paquete
**nodejs** podra dar problemas.

Yarn
****

* https://yarnpkg.com/en/docs/install

.. code-block:: bash

    sudo wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
    sudo dnf install -y yarn

Paquetes que instalo
********************

Los linters, se instalan a nivel local.

.. code-block:: bash

    # Comunes
    sudo npm i -g bower
    sudo npm i -g gulp
    sudo npm i -g node-sass

    # Linters
    # sudo npm i -g eslint
    # sudo npm i -g htmlhint
    # sudo npm i -g stylelint
    # sudo npm i -g stylelint-config-standard

Algunos comandos utiles
***********************

.. code-block:: bash

    # Muestra los paquetes para actualizar (no actualizar npm)
    npm outdated -g --depth=0

    # Listar todos los paquetes
    npm list -g --depth=0
