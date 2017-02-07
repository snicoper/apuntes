.. _reference-linux-python-instalacion_python_fedora:

############################
Instalación Python en Fedora
############################

Python3
=======

.. code-block:: bash

    su
    dnf install -y python3-setuptools python3-devel redhat-rpm-config

Virtualenvwrapper
*****************

.. code-block:: bash

    # pip3 install virtualenvwrapper
    dnf install -y python3-virtualenvwrapper

Editar ``.bashrc``

.. code-block:: bash

    vim ~/.bashrc

    # Virtualenvwrapper
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    export WORKON_HOME=$HOME/.virtualenvs
    source /usr/bin/virtualenvwrapper.sh

En ``source`` el valor de ``which virtualenvwrapper.sh``

Reload ``~/.bashrc``

.. code-block:: bash

    # Guardar y salir
    source ~/.bashrc

Entorno virtual **default**

.. code-block:: bash

    mkvirtualenv default

    (default) pip install -U \
        autopep8 \
        Django \
        flake8 \
        isort \
        pydocstyle \
        Sphinx \
        sphinx-autobuild \
        sphinx-rtd-theme

Comandos

* mkvirtualenv // Crea un nuevo virtualenv
* rmvirtualenv // Elimina un virtualenv existente
* workon nombre_env // Activar entorno virtual, si se omite nombre_env, mostrara todos los disponibles
* deactivate // Desactivar virtualenv
* lsvirtualenv // Listar virtualenvs

Python 3.4 en Centos 7
######################

.. code-block:: bash

    yum install epel-release

    yum install python34 python34-setuptools python34-devel redhat-rpm-config

    curl https://bootstrap.pypa.io/get-pip.py | python3.4
