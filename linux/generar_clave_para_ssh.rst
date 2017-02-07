.. _reference-linux-generar_clave_para_ssh:

######################
Generar clave para SSH
######################

.. code-block:: bash

    ssh-keygen -t rsa -b 4096

    # Agregar clave SSH al agente ssh (evitar tener que poner el passphrase siempre)
    ssh-add

Si ``ssh-add`` devuelve **Could not open a connection to your authentication agent.**

.. code-block:: bash

    eval `ssh-agent -s`
    ssh-add

El directorio ~/.ssh debe tener permisos 700 y los archivos de dentro de ~/.ssh han de ser de 600

.. code-block:: bash

    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/*
