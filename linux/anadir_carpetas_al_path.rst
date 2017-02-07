.. _reference-linux-anadir_carpetas_al_path:

##########################
Añadir directorios al PATH
##########################

Editar ~/.bashrc

.. code-block:: bash

    vim ~/.bashrc

Añadir al final

.. code-block:: bash

    PATH="$PATH:/data/myscripts"
    export PATH

    # También
    export PATH="$PATH:/data/myscripts"
