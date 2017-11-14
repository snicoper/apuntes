.. _reference-programacion-postgresql-comandos_consola_psql:

#########################
Comandos consola Postgres
#########################

.. note::
    Cuando usa ``$``, significa que esta en el shell, cuando no tiene nada
    es que esta en psql

Login usuario postgres:

.. code-block:: bash

    $ sudo su - postgres

Creación de un usuario:

.. code-block:: bash

    CREATE USER nombre_usuario WITH password '123456'

Eliminar usuario:

.. code-block:: bash

    DROP USER nombre_usuario


Crear base de datos:

.. code-block:: bash

    CREATE DATABASE nombre_db WITH OWNER nombre_usuario;

Eliminar base de datos:

.. code-block:: bash

    DROP DATABASE nombre_db

Acceder database con usuario x:

.. code-block:: bash

    psql -U nombre_usuario nombre_db

Obtener ayuda:

.. code-block:: bash

    \h

Quit

.. code-block:: bash

    \q

Leer comandos desde un archivo:

.. code-block:: bash

    \i input.sql

Dump db a un archivo:

.. code-block:: bash

    $ pg_dump -U nombre_usuario nombre_db > db.out

Dump todas las bases de datos:

.. code-block:: bash

    $ sudo su - postgres
    $ pg_dumpall > /var/lib/pgsql/backups/dumpall.sql

Restaurar db:

.. code-block:: bash

    $ sudo su - postgres
    $ psql -f /var/lib/pgsql/backups/dumpall.sql mydb

También:

.. code-block:: bash

    $ psql -U postgres nombredb < archivo_restauracion.sql

List databases:

.. code-block:: bash

    \l

List tables in database:

.. code-block:: bash

    \d

Describe table:

.. code-block:: bash

    \d table_name

Describe table:

.. code-block:: bash

    \d+ table_name

Use database_name:

.. code-block:: bash

    \c nombre_db

Show users:

.. code-block:: bash

    select * from "pg_user";
    # también
    \du

Escribir las consultas en tu editor favorito:

.. code-block:: bash

    \e

Activar/Desactivar ver el tiempo del query:

.. code-block:: bash

    \timing

Reset a user password as admin:

.. code-block:: bash

    ALTER USER usertochange WITH password 'new_passwd';

Select version

.. code-block:: bash

    SELECT version();

Change Database Owner:

.. code-block:: bash

    ALTER DATABASE database_name OWNER TO new_owner;

Create a superuser user:

.. code-block:: bash

    ALTER USER mysuper WITH SUPERUSER;
    # or even better
    ALTER USER mysuper WITH SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN REPLICATION

Saber el tamaño usado las tablas en una base de datos:

Ver mas:
http://www.niwi.be/2013/02/17/postgresql-database-table-indexes-size/

.. code-block:: bash

    SELECT pg_size_pretty(pg_database_size('dbname'));
