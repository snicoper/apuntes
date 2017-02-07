.. _reference-linux-python-instalar_python:

############################
Instalacion Python en Ubuntu
############################

Python3
=======

.. code-block:: bash

    sudo apt install -y python3 python3-dev python3-setuptools python3-pip

Virtualenvwrapper
*****************

.. code-block:: bash

    sudo pip3 install virtualenvwrapper

    mkdir ~/.virtualenvs

Editar .bashrc

.. code-block:: bash

    vim ~/.bashrc

Añadir

.. code-block:: bash

    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    export WORKON_HOME=$HOME/.virtualenvs
    source /usr/local/bin/virtualenvwrapper.sh

En ``source`` el valor de ``which virtualenvwrapper.sh``

Comandos

* mkvirtualenv // Crea un nuevo virtualenv
* rmvirtualenv // Elimina un virtualenv existente
* workon // Cambia el actual virtualenv
* deactivate // Desactivar virtualenv
* lsvirtualenv // Listar virtualenvs

