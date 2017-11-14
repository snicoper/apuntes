.. _reference-linux-python-instalar_python:

############################
Instalación Python en Ubuntu
############################

Python3
=======

.. code-block:: bash

    sudo apt install -y python3 python3-dev python3-setuptools python3-pip

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
