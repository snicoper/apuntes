.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

De **nodesource**

* https://nodejs.org/es/download/package-manager/#enterprise-linux-y-fedora

.. code-block:: bash

    curl -sL https://rpm.nodesource.com/setup_9.x | bash -
    dnf install -y nodejs

Donde ``setup_9.x``, poner la versión estable.

De los repositorios de la distro.

.. code-block:: bash

    sudo dnf -y install nodejs

Yarn
****

* https://yarnpkg.com/en/docs/install

.. code-block:: bash

    sudo wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
    sudo dnf install -y yarn

Añadir ``~/.yarn/bin`` al **PATH**

.. code-block:: bash

    # ~/.bashrc
    export PATH=$PATH:~/.yarn/bin

Paquetes que instalo
********************

.. code-block:: bash

    # Comunes
    # Con yarn, sin sudo: yarn global add gulp node-sass eslint htmlhint stylelint stylelint-config-standard
    sudo npm i -g gulp
    sudo npm i -g node-sass

    # Linters
    sudo npm i -g eslint
    sudo npm i -g htmlhint
    sudo npm i -g stylelint
    sudo npm i -g stylelint-config-standard

Algunos comandos utiles npm
***************************

.. code-block:: bash

    # Muestra los paquetes para actualizar (no actualizar npm)
    npm outdated -g --depth=0

    # Listar todos los paquetes
    npm list -g --depth=0
