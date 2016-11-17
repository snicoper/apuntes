.. _reference-linux-instalar-golang:

###############
Instalar Golang
###############

.. code-block:: bash

    sudo dnf install golang


Obtener la ultima version https://golang.org/dl/
.. code-block:: bash

    sudo tar -C /usr/local -xzf go1.7.1.linux-amd64.tar.gz

Añadir al ``PATH``

.. code-block:: bash

    vim ~/.bashrc

    # Golang
    export PATH=$PATH:/usr/local/go/bin
    export GOPATH=$HOME/.go