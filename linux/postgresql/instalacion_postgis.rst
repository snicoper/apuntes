.. _reference-linux-postgresql-instalacion_postgis:

######################
Instalación de Postgis
######################

**Fuentes**

* http://postgis.net/docs/postgis_installation.html

--------

.. code-block:: bash

    dnf -y install postgis

Es necesario habilitar cada base de datos

.. code-block:: bash

    psql -U postgres -c "CREATE DATABASE nombre_database WITH OWNER nombre_usuario;"
    psql -U postgres -d nombre_database -c "CREATE EXTENSION postgis;"
    psql -U postgres -d nombre_database -c "CREATE EXTENSION postgis_topology;"
    psql -U postgres -d nombre_database -c "SELECT postgis_version();"
