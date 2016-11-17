.. _reference-linux-python-pip_upgrade_all_packages:

####################################
Actualizar todos los paquetes de Pip
####################################

.. code-block:: bash

    pip freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs pip install -U

Tambien se puede crear un archivo ``pip-upgrade-all``

.. code-block:: bash

    vim pip-upgrade-all

.. code-block:: bash

    #!/bin/bash
    # Actualiza todos los paquetes pip de un entorno virtual.
    # Primero genera un archivo en el directorio actual, con los
    # paquetes.
    # Después actualiza todos los paquetes a la ultima versión.

    env_name=$(basename "$VIRTUAL_ENV")

    if [ -n "$env_name" ]
    then
      path_backup="${PWD}/pip-${env_name}-backup.txt"

      # Creara un backup con las versiones actuales, por si pasa algo.
      pip freeze > $path_backup

      pip freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs pip install -U
    else
      echo "No estas en un entorno virtual"
    fi

    read -p "Eliminar ${path_backup}(y/[N]) " yn
    if [ "$yn" == "y" -o "$yn" == "Y" ]
    then
      rm -f $path_backup
    fi

Dar permisos de ejecución

.. code-block:: bash

    chmod +x pip-upgrade-all

y moverlo a ``/usr/bin/``

.. code-block:: bash

    sudo mv pip-upgrade-all /usr/bin/pip-upgrade-all

Ahora desde cualquier entorno virtual.

.. code-block:: bash

    (myenv) pip-upgrade-all
