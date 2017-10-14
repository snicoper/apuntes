.. _reference-linux-python-instalacion_python_fedora:

############################
Instalación Python en Fedora
############################

Python3
=======

.. code-block:: bash

    dnf install -y python3-setuptools python3-devel redhat-rpm-config

Virtualenvwrapper
*****************

.. code-block:: bash

    # Como usuario
    pip3 install --user virtualenvwrapper

Editar ``.bashrc``

.. code-block:: bash

    which python3
    which virtualenvwrapper.sh

.. code-block:: bash

    vim ~/.bashrc

    # Virtualenvwrapper
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    export WORKON_HOME=$HOME/.virtualenvs
    source ~/.local/bin/virtualenvwrapper.sh

.. code-block:: bash

    source ~/.bashrc

Entorno virtual **default**

.. code-block:: bash

    mkvirtualenv default

    (default) pip install -U \
        autopep8 \
        Django \
        flake8 \
        isort \
        livereload \
        pycodestyle \
        pydocstyle \
        Sphinx \
        sphinx-autobuild \
        sphinx-rtd-theme

**Comandos**

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

Python 3.6 en Centos 7
######################

**No lo he probado**

* https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-centos-7
