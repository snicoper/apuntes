.. _reference-linux-postgresql-postgres_last_version_centos7:


########################################
Ultima version de PostgreSQL en Centos 7
########################################

.. warning:: Solo he probado con **PostgreSQL 9.6.X**


Elegir la versión en `repopackages`_

.. _repopackages: https://yum.postgresql.org/repopackages.php

.. code-block:: bash

    yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm

    yum install postgresql96 postgresql96-server postgresql96-devel postgresql96-contrib postgis2_96

Si es la única version de PostgreSQL, añadir al **PATH**.

.. code-block:: bash

    vim /etc/profile

    export PATH="$PATH:/usr/pgsql-9.6/bin/"

    # Reiniciar

    postgresql96-setup initdb
    systemctl start postgresql-9.6
    systemctl enable postgresql-9.6

    # Añadir contraseña a postgres.
    su - postgres
    psql
    \password postgres
    \q
    exit

Archivos de configuración

.. code-block:: bash

    vim /var/lib/pgsql/9.6/data/postgresql.conf
    vim /var/lib/pgsql/9.6/data/pg_hba.conf

