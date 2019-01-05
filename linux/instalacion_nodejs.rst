.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

De **nodesource**

* https://nodejs.org/es/download/package-manager/#enterprise-linux-y-fedora

.. code-block:: bash

    curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -
    dnf install -y nodejs

Donde ``setup_10.x``, poner la versión estable.

De los repositorios de la distro.

.. code-block:: bash

    dnf -y install nodejs

Yarn
****

* https://yarnpkg.com/en/docs/install

.. code-block:: bash

    curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
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
    yarn global add \
        @angular/cli \
        @vue/cli \
        gulp \
        node-sass

    # NPM con sudo
    sudo npm i -g gulp
    sudo npm i -g node-sass

Establecer yarn predeterminado con ``ng``

.. code-block:: bash

    ng config -g cli.packageManager yarn

Para aumentar el tamaño de monitoreo de **inotify**

.. code-block:: bash

    echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
