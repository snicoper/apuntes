.. _reference--windows-pgpass_windows:

#################
pgpass en windows
#################

.. code-block:: bash

    echo %APPDATA%

    # C:\Users\snicoper\AppData\Roaming

Crear directorio ``postgresql`` en ``C:\Users\snicoper\AppData\Roaming``

Añadir ``pgpass.conf``

.. code-block:: bash

    hostname:port:database:username:password
