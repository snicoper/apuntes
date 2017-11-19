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
        restructuredtext-lint \
        Sphinx \
        sphinx-autobuild \
        sphinx-rtd-theme

Comandos virtualenvwrapper
==========================

* ``mkvirtualenv`` Crea un nuevo virtualenv
* ``rmvirtualenv`` Elimina un virtualenv existente
* ``workon`` Cambia el actual virtualenv
* ``deactivate`` Desactivar virtualenv
* ``lsvirtualenv`` Listar virtualenvs
