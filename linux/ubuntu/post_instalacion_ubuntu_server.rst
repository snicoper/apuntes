.. _reference-linux-ubuntu-post_instalacion_ubuntu_server:

##############################
Post instalacion Ubuntu Server
##############################

Crear usuario
*************

.. code-block:: bash

    adduser snicoper
    passwd snicoper

    sudo adduser snicoper sudo

hostname
********

.. code-block:: bash

    hostnamectl --static set-hostname fqdn.host.name

Timezone
********

.. code-block:: bash

    timedatectl set-timezone Europe/Madrid

Cambiar Keyboard Layout (keymap)
*********************************

.. code-block:: bash

    locale-gen es_ES.UTF-8

    localectl list-locales | grep es

Para cambiar a ``es``

.. code-block:: bash

    localectl set-keymap es_ES.utf8

Instalar Vim.
*************

.. code-block:: bash

    sudo apt -y install vim

Cambiar editor.

.. code-block:: bash

    sudo update-alternatives --config editor

Recordar ultima posición.

.. code-block:: bash

    vim /etc/vim/vimrc

    # Descomentar lineas, 29, 30 y 31
    " Uncomment the following to have Vim jump to the last position when
    " reopening a file
    if has("autocmd")
      au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
    endif

Habilitar ufw (firewall)
************************

.. code-block:: bash

    sudo ufw allow 22
    sudo ufw enable

Actualizar
**********

Cambiar a servers Francia.

.. code-block:: bash

    sudo vim /etc/apt/sources.list

Actualizar

.. code-block:: bash

    sudo apt update && sudo apt dist-upgrade

Paquetes básicos
****************

.. code-block:: bash

    sudo apt install -y \
        build-essential \
        git \
        curl \
        wget \
        ssh \
        htop \
        nmap \
        tree
