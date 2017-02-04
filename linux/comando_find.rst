.. _reference-linux-comando_find:

############
Comando find
############

Comando ``find``, directorio ``./``, patron ``-name``, archivo o directorio ``-type f|d``, comando a ejecutar ``-exec comando`` {} \\;

**Algunos ejemplos**

Dar permisos 777 a todos los archivos recursivamente desde la posición actual.

.. code-block:: bash

    find ./ -name '*.php' -type f -exec chmod 777 {} \;

Eliminar recursivamente archivos con X nombre desde la posición actual.

.. code-block:: bash

    find ./ -name '*.php' -type f -exec rm -f {} \;

Cambiar de permisos recursivamente desde la posición actual.

.. code-block:: bash

    find ./ -type f -exec dos2unix {} \;
