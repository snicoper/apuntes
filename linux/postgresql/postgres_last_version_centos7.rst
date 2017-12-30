.. _reference-linux-postgresql-postgres_last_version_centos7:

############################
Ultima version de PostgreSQL
############################

Elegir la versión en `repopackages`_

.. _repopackages: https://yum.postgresql.org/repopackages.php

Versión para los apuntes **PostgreSQL 10**

Fedora
======

.. code-block:: bash

    dnf install https://download.postgresql.org/pub/repos/yum/10/fedora/fedora-27-x86_64/pgdg-fedora10-10-3.noarch.rpm

    dnf install postgresql10 postgresql10-server postgresql10-devel postgresql10-contrib pgadmin4-v2

    # Postgis
    dnf install postgis2_10

Centos
======

.. code-block:: bash

    yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm

    yum install postgresql10 postgresql10-server postgresql10-devel postgresql10-contrib

    # Postgis
    yum install postgis2_10

Añadir al PATH
==============

.. code-block:: bash

    vim /etc/profile

    export PATH="$PATH:/usr/pgsql-10/bin/"

    # Requiere reiniciar

    postgresql-10-setup initdb
    systemctl start postgresql-10
    systemctl enable postgresql-10

    # Añadir contraseña a postgres.
    su - postgres
    psql
    \password postgres
    \q
    exit

Archivos de configuración

.. code-block:: bash

    vim /var/lib/pgsql/10/data/postgresql.conf
    vim /var/lib/pgsql/10/data/pg_hba.conf

:ref:`reference-linux-postgresql-instalacion_postgresql`

.. code-block:: bash

    systemctl restart postgresql-10
