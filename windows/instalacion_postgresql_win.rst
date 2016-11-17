.. _reference--windows-instalacion_postgresql_win:

#################################
Instalación de PostgreSQL Windows
#################################

Fuentes
*******

* http://www.postgresql.org/

* http://www.petrikainulainen.net/programming/tips-and-tricks/installing-postgresql-9-1-to-windows-7-from-the-binary-zip-distribution/

* http://www.pgadmin.org/

------------------------

.. note::
    Para una instalación rápida, descargar el instalador y solo añadirlo al ``PATH``,
    me creo la menera del ``.zip`` por pura curiosidad.

    La versión probada es **9.3.4**, cambiar según versión.

* Descargar el archivo ``.zip``
* Crear carpeta ``C:\Postgresql``
* Descomprimir carpeta en ``C:\Postgresql``
* Renombrar ``C:\Postgresql\pgsql`` a ``C:\Postgresql\9.3.4``
* Crear dentro de ``C:\Postgresql\9.3.4`` dos directorios

.. code-block:: none

    data
    log

Añadir el PATH
**************

.. code-block:: none

    C:\Postgresql\9.3.4\bin;

CMD
***

Inicializar data
================

.. code-block:: none

    initdb -U postgres -A password -E utf8 -W -D C:\Postgresql\9.3.4\data

Iniciar
=======

.. code-block:: none

    pg_ctl -D "C:/Postgresql/9.3.4/data" -l "C:/Postgresql/9.3.4/log/pgsql.log" start

Parar
=====

    pg_ctl -D "C:/Postgresql/9.3.4/data" -l "C:/Postgresql/9.3.4/log/pgsql.log" stop

Añadir como Servicio
********************

.. code-block:: none

    pg_ctl.exe register -N Postgresql -U "NT AUTHORITY\NetworkService" -D "C:/Postgresql/9.3.4/data" -w

Descargar e instalar pgadmin
****************************

* http://www.pgadmin.org/

Configurar
**********

Abrir ``C:\Postgresql\9.3.4\data\postgresql.conf``

.. code-block:: none

    # Descomentar
    listen_addresses = 'localhost'
    port = 5432

Crear base de datos ``practicas`` y usuario ``snicoper``

.. code-block:: none

    psql -U postgres
    CREATE USER snicoper WITH PASSWORD '123456' NOCREATEDB NOCREATEUSER;
    CREATE DATABASE practicas WITH OWNER = snicoper;

.. note::
    Para evitar el mensaje en cmd

    .. code-block:: none

        ADVERTENCIA: El código de página de la consola (850) difiere del código
            de página de Windows (1252).
            [...]

    En CMD poner

    .. code-block:: none

        /c chcp 1252
