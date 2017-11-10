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
    yum install epel-release

    # remi
    yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

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

Útiles
******

* ``PostgreSQL`` :ref:`reference-linux-postgresql-postgres_last_version_centos7`
* ``Python 3.6`` :ref:`reference-linux-python-python_last_centos`
* ``Nginx`` :ref:`reference-linux-nginx-instalacion_nginx`
