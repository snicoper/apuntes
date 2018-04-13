.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

De **nodesource**

* https://nodejs.org/es/download/package-manager/#enterprise-linux-y-fedora

.. code-block:: bash

    curl --silent --location https://rpm.nodesource.com/setup_9.x | bash -
    dnf install -y nodejs

Donde ``setup_9.x``, poner la versión estable.

De los repositorios de la distro.

.. code-block:: bash

    dnf -y install nodejs

Yarn
****

* https://yarnpkg.com/en/docs/install

.. code-block:: bash

    wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
    dnf install -y yarn

Añadir ``~/.yarn/bin`` al **PATH**

.. code-block:: bash

    # ~/.bashrc
    export PATH=$PATH:~/.yarn/bin

Paquetes que instalo
********************

.. code-block:: bash

    # Comunes
    # Con yarn, como usuario:
    yarn global add gulp node-sass eslint htmlhint stylelint stylelint-config-standard

    # NPM con sudo
    sudo npm i -g gulp
    sudo npm i -g node-sass

    # Linters
    sudo npm i -g eslint
    sudo npm i -g htmlhint
    sudo npm i -g stylelint
    sudo npm i -g stylelint-config-standard
