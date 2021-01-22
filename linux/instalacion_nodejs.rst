.. _reference-linux-instalacion_nodejs:

##################
Instalación NodeJS
##################

Instalación
***********

De **nodesource**

* https://nodejs.org/es/download/package-manager/#enterprise-linux-y-fedora

.. code-block:: bash

    curl -sL https://rpm.nodesource.com/setup_12.x | bash -
    dnf install -y nodejs

De los repositorios de la distro.

.. code-block:: bash

    dnf -y install nodejs

npm global directorio de usuario
********************************

* https://stackoverflow.com/a/13021677

.. code-block:: bash

    # Como usuario
    NPM_PACKAGES="$HOME/.npm-packages"
    mkdir -p "$NPM_PACKAGES"

    echo "prefix = $NPM_PACKAGES" >> ~/.npmrc

Editar ``.zshrc`` o ``.bashrc``

.. code-block:: bash

    # NPM packages in homedir
    NPM_PACKAGES="$HOME/.npm-packages"

    # Tell our environment about user-installed node tools
    PATH="$NPM_PACKAGES/bin:$PATH"

    # Unset manpath so we can inherit from /etc/manpath via the `manpath` command
    unset MANPATH  # delete if you already modified MANPATH elsewhere in your configuration
    MANPATH="$NPM_PACKAGES/share/man:$(manpath)"

    # Tell Node about these packages
    NODE_PATH="$NPM_PACKAGES/lib/node_modules:$NODE_PATH"

Yarn
****

* https://yarnpkg.com/en/docs/install

.. code-block:: bash

    npm install -g yarn

Para aumentar el tamaño de monitoreo de **inotify**

.. code-block:: bash

    # Limite temporal
    sudo sysctl fs.inotify.max_user_watches=524288

    # Limite permanente
    echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
