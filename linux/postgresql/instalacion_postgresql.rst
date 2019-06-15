.. _reference-linux-postgresql-instalacion_postgresql:

#########################
Instalación de PostgreSQL
#########################

Fedora y Centos
***************

:ref:`reference-linux-postgresql-postgres_last_version_centos7`

Instalación

.. code-block:: bash

    dnf install -y postgresql postgresql-server postgresql-devel postgresql-contrib

.. code-block:: bash

    # Centos
    # postgresql-setup initdb

    # Fedora
    postgresql-setup --initdb --unit postgresql

    systemctl enable postgresql.service
    systemctl start postgresql.service

Establecer contraseña de postgres

.. code-block:: bash

    su - postgres
    psql
    \password postgres

    CREATE USER snicoper WITH PASSWORD '123456' CREATEDB;
    CREATE DATABASE practicas WITH OWNER snicoper;
    \q
    exit

Configuración

.. code-block:: bash

    vim /var/lib/pgsql/data/postgresql.conf

.. code-block:: bash

    # linea 59
    listen_addresses = 'localhost'

    # linea 63 descomentar
    port = 5432

.. code-block:: bash

    vim  /var/lib/pgsql/data/pg_hba.conf

Remplazar toda la parte siguiente al final del archivo

.. code-block:: bash

    # TYPE  DATABASE        USER            ADDRESS                 METHOD

    # "local" is for Unix domain socket connections only
    local   all         all                               md5
    # IPv4 local connections:
    host    all         all         127.0.0.1/32          md5
    # IPv6 local connections:
    host    all         all         ::1/128               md5

.. code-block:: bash

    systemctl restart postgresql.service

Ver :ref:`reference-linux-fedora-centos-reglas_selinux`
