.. _reference-linux-python-python_last_centos:

###################
Python 3.6 Centos 7
###################

Varias formas para tener ultima version de Python 3 en Centos 7.

----

Compilando fuentes
==================

.. note::

    Con la **version 3.6** no lo he probado.

* :ref:`reference-linux-fedora-centos-post_instalacion_centos`

.. code-block:: bash

    sudo yum install \
        zlib-devel \
        bzip2-devel \
        openssl-devel \
        ncurses-devel \
        sqlite-devel \
        readline-devel \
        tk-devel \
        gdbm-devel \
        db4-devel \
        libpcap-devel \
        xz-devel

.. code-block:: bash

    sudo echo "/usr/local/lib" >> /etc/ld.so.conf

.. code-block:: bash

    wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz
    tar -zxvf Python-3.6.3.tgz
    cd Python-3.6.3

    ./configure --prefix=/usr/local --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib"
    make
    sudo make altinstall

iuscommunity
============

* https://ius.io/
* https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-centos-7
* :ref:`reference-linux-fedora-centos-post_instalacion_centos`

.. code-block:: bash

    yum -y install yum-utils

.. code-block:: bash

    yum -y install https://centos7.iuscommunity.org/ius-release.rpm
    yum -y install python36u python36u-pip python36u-devel


software collections
====================

* https://www.softwarecollections.org/en/

Esta forma no la conozco bien, ademas **virtualenvwrapper** no he conseguido instalarlo, aunque
si **virtualenv**.

¿Para un servidor de producción, quiza **virtualenvwrapper** no sea del todo necesario?

.. code-block:: bash

    yum install centos-release-scl
    yum-config-manager --enable rhel-server-rhscl-7-rpms
    yum install rh-python36
    scl enable rh-python36 bash

Me falta probarlo mas...

Python 3.4 epel
###############

.. code-block:: bash

    yum install epel-release

    yum install python34 python34-setuptools python34-devel redhat-rpm-config

    curl https://bootstrap.pypa.io/get-pip.py | python3.4

Virtualenvwrapper
=================

Como usuario:

.. code-block:: bash

    pip3.6 install --user virtualenvwrapper

Editar ``.bashrc``

.. code-block:: bash

    which python3.6
    which virtualenvwrapper.sh

.. code-block:: bash

    vim ~/.bashrc

    # Virtualenvwrapper
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    export WORKON_HOME=$HOME/.virtualenvs
    source ~/.local/bin/virtualenvwrapper.sh

.. code-block:: bash

    source ~/.bashrc

Comandos virtualenvwrapper
==========================

* ``mkvirtualenv`` Crea un nuevo virtualenv
* ``rmvirtualenv`` Elimina un virtualenv existente
* ``workon`` Cambia el actual virtualenv
* ``deactivate`` Desactivar virtualenv
* ``lsvirtualenv`` Listar virtualenvs
