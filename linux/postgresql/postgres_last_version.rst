.. _reference-linux-postgresql-postgres_last_version_centos7:

############################
Ultima version de PostgreSQL
############################

Elegir la versión en `repopackages`_

.. _repopackages: https://yum.postgresql.org/repopackages.php

Versión para los apuntes **PostgreSQL 11**

Fedora
======

.. code-block:: bash

    dnf install https://download.postgresql.org/pub/repos/yum/testing/12/fedora/fedora-29-x86_64/pgdg-fedora12-12-1.noarch.rpm

    dnf install postgresql11 postgresql11-server postgresql11-devel postgresql11-contrib pgadmin4-v2

    # Postgis
    dnf install postgis2_11

Centos
======

.. code-block:: bash

    yum install https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-x86_64/pgdg-centos11-11-2.noarch.rpm

    yum install postgresql11 postgresql11-server postgresql11-devel postgresql11-contrib

    # Postgis
    yum install postgis2_11

Añadir al PATH
==============

.. code-block:: bash

    vim /etc/profile

    export PATH="$PATH:/usr/pgsql-11/bin/"

    # Requiere reiniciar

    postgresql-11-setup initdb
    systemctl start postgresql-11
    systemctl enable postgresql-11

    # Añadir contraseña a postgres.
    su - postgres
    psql
    \password postgres
    \q
    exit

Archivos de configuración

.. code-block:: bash

    vim /var/lib/pgsql/11/data/postgresql.conf
    vim /var/lib/pgsql/11/data/pg_hba.conf

:ref:`reference-linux-postgresql-instalacion_postgresql`

.. code-block:: bash

    systemctl restart postgresql-11
