.. _reference-linux-python-compilar_python_34_centos:

#################################
Compilar Python 3.6.3 en Centos 7
#################################

.. note::

    Con la version 3.6 no lo he probado.

Compilación
***********

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

Usar pip con ``pip3.6``

Virtualenvwrapper
*****************

Como usuario:

.. code-block:: bash

    # Como usuario
    pip3.6 install --user virtualenvwrapper
    exit

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

Comandos

* mkvirtualenv // Crea un nuevo virtualenv
* rmvirtualenv // Elimina un virtualenv existente
* workon // Cambia el actual virtualenv
* deactivate // Desactivar virtualenv
* lsvirtualenv // Listar virtualenvs

