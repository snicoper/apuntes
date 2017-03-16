.. _reference-linux-postgresql-pgadmin4_virtualenv:

##########################
pgAdmin4 virtualenvwrapper
##########################

**Fuentes**

* http://askubuntu.com/questions/831262/how-to-install-pgadmin-4-in-desktop-mode-on-ubuntu-16-04

-----

Para ver las versiones https://www.pgadmin.org/download/pip4.php

Descargar el archivo segun version.

.. code-block:: bash

    cd Downloads
    wget https://ftp.postgresql.org/pub/pgadmin3/pgadmin4/v1.3/pip/pgadmin4-1.3-py2.py3-none-any.whl

Crear el entorno virtual

.. code-block:: bash

    mkvirtualenv pgAdmin4

Instalar

.. code-block:: bash

    pip install pgadmin4-1.3-py2.py3-none-any.whl

**Por hacer**

-----

El archivo esta en ``lib/python2.7/site-packages/pgadmin4/pgAdmin4.py``, crear enlace a un directorio ``$PATH``

**Ver** http://askubuntu.com/questions/831262/how-to-install-pgadmin-4-in-desktop-mode-on-ubuntu-16-04

``echo "SERVER_MODE = False" >> lib/python2.7/site-packages/pgadmin4/config_local.py``