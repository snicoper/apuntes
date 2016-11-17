.. _reference-linux-postgresql-instalacion_postgresql:

#########################
Instalación de PostgreSQL
#########################

Fuentes
*******

* https://help.ubuntu.com/community/PostgreSQL

Fedora y Centos
***************

Instalación

.. code-block:: bash

    dnf install -y postgresql postgresql-server postgresql-devel

    # Opcional
    dnf install -y pgadmin3

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

    CREATE USER snicoper WITH PASSWORD '123456' NOCREATEDB NOCREATEUSER;
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

Ubuntu
******

Instalación

.. code-block:: bash

    sudo apt install -y postgresql postgresql-contrib libpq-dev

    # Opcional
    sudo apt install -y pgAdmin3

Establecer contraseña de postgres

.. code-block:: bash

    su - postgres
    psql
    \password postgres

    CREATE USER snicoper WITH PASSWORD '123456' NOCREATEDB NOCREATEUSER;
    CREATE DATABASE practicas WITH OWNER snicoper;
    \q
    exit

Configuración PostgreSQL

.. code-block:: bash

    sudo vim /etc/postgresql/9.5/main/postgresql.conf

.. code-block:: bash

    # Descomentar, linea 59
    listen_addresses = 'localhost'

    # Descomentar, linea 89
    password_encryption = on

.. code-block:: bash

    sudo vim /etc/postgresql/9.5/main/pg_hba.conf

.. code-block:: bash

    # "local" is for Unix domain socket connections only
    local   all         all                               md5

.. code-block:: bash

    sudo service postgresql restart
