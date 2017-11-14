.. _reference-linux-python-pip_upgrade_all_packages:

####################################
Actualizar todos los paquetes de Pip
####################################

.. code-block:: bash

    pip freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs pip install -U

También se puede crear un archivo ``pip-upgrade-all``

.. code-block:: bash

    vim pip-upgrade-all

.. code-block:: bash

    #!/bin/bash
    # Actualiza todos los paquetes pip de un entorno virtual.

    ENV_NAME=$(basename "$VIRTUAL_ENV")
    OUTPUT="$(pip list --outdate)"

    if [ -n "$ENV_NAME" ]
    then
      PATH_BACKUP="${PWD}/pip-${ENV_NAME}-backup.txt"

      # Creara un backup con las versiones actuales, por si pasa algo.
      pip freeze > $PATH_BACKUP

      pip freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs pip install -U

      echo "$OUTPUT"
    else
      echo "No estas en un entorno virtual"
    fi

    read -p "Eliminar ${PATH_BACKUP}(y/[N]) " yn
    if [ "$yn" == "y" -o "$yn" == "Y" ]
    then
      rm -f $PATH_BACKUP
    fi

Dar permisos de ejecución y mover a ``/usr/bin/``

.. code-block:: bash

    chmod +x pip-upgrade-all
    sudo mv pip-upgrade-all /usr/bin/pip-upgrade-all

Ahora desde cualquier entorno virtual.

.. code-block:: bash

    (myenv) pip-upgrade-all
