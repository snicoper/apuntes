.. _reference-linux-cat_con_texto_coloreado:

###############################
Comando Cat con texto coloreado
###############################

Desde los repositorios

.. code-block:: bash

    # Fedora/Centos
    yum install python-pygments

    # Ubuntu
    apt-get install python-pygments

Con Pip

ver :ref:`reference-linux-python-instalar_python`

.. code-block:: bash

    # Python 2
    pip install Pygments

    # Python 3
    pip3 install Pygments

Editar ~/.bashrc y añadir alias

.. code-block:: bash

    alias ccat='pygmentize -g'
