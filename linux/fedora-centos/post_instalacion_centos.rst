.. _reference-linux-fedora-centos-post_instalacion_centos:

#########################
Post instalación Centos 7
#########################

.. note::
    Centos 7 Minimal. Todo como super usuario.

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
    yum install -y epel-release

    # remi
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm

Actualizar el sistema
*********************

.. code-block:: bash

    yum -y update

Programas básicos
*****************

.. code-block:: bash

    yum -y install \
        bash-completion \
        cpp \
        firewalld \
        gcc \
        git \
        htop \
        kernel-devel \
        kernel-headers \
        make \
        mutt \
        net-tools \
        openssh \
        policycoreutils-python \
        vim \
        wget \
        yum-utils

Enable Firewalld
================

.. code-block:: bash

    systemctl start firewalld.service
    systemctl enable firewalld.service

bash-git-prompt
===============

* https://github.com/magicmonty/bash-git-prompt

.. code-block:: bash

    cd ~
    git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1

.. code-block:: bash

    vim ~/.bashrc

    GIT_PROMPT_ONLY_IN_REPO=0
    source ~/.bash-git-prompt/gitprompt.sh

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
