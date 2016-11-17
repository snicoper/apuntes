.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

.. code-block:: bash

    sudo dnf -y install nodejs npm

Si después se actualiza **npm** con ``sudo npm install npm -g`` a la hora de actualizar el paquete
**nodejs** dará problemas.

Paquetes que instalo
====================

Los linters, se instalan a nivel local en los proyectos, no son necesarios.

.. code-block:: bash

    # Comunes
    sudo npm install -g bower
    sudo npm install -g gulp
    sudo npm install -g node-sass

    # Opcionales
    sudo npm install -g npm-check-updates
    sudo npm install -g babel-cli
    sudo npm install -g webpack

    # Linters
    sudo npm install -g eslint
    sudo npm install -g htmlhint
    sudo npm install -g stylelint
    sudo npm install -g stylelint-config-standard

Algunos comandos utiles
***********************

.. code-block:: bash

    # Muestra los paquetes para actualizar (no actualizar npm)
    npm outdated -g --depth=0

    # Listar todos los paquetes
    npm list -g --depth=0
