.. _reference-linux-fedora-centos-post_instalacion_centos:

#########################
Post instalación Centos 8
#########################

.. note::
    Centos 8 Minimal. Todo como super usuario.

Crear usuario y añadir a wheel
*******************************

.. code-block:: bash

    adduser snicoper
    passwd snicoper

    usermod -aG wheel snicoper

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

    localectl list-keymaps | grep es

Para cambiar a ``es``

.. code-block:: bash

    localectl set-keymap es

REMI y EPEL RHEL/CentOS 7
*************************

.. code-block:: bash

    # epel
    dnf install -y epel-release

    # remi
    dnf install -y http://rpms.remirepo.net/enterprise/remi-release-8.rpm

Actualizar el sistema
*********************

.. code-block:: bash

    dnf -y update

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        bash-completion \
        bashtop \
        cpp \
        gcc \
        git \
        htop \
        kernel-devel \
        kernel-headers \
        make \
        mutt \
        util-linux-user \
        wget \
        yum-utils \
        zsh

Útiles
******

* :ref:`reference-linux-fedora-centos-configurar_ssh`
* :ref:`reference-editors-vim-mi_vimrc`
* :ref:`reference-git-gitconfig_linux`
* :ref:`reference-linux-mi_bashrc`
* :ref:`reference-linux-postgresql-postgres_last_version_centos7`
* :ref:`reference-linux-python-python_last_centos`
* :ref:`reference-linux-nginx-instalacion_nginx`
* :ref:`reference-linux-fedora-centos-certificado_lets_encrypt`
* :ref:`reference-linux-fedora-centos-postfix`
* :ref:`reference-linux-fedora-centos-bind_fedora`
