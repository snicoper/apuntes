.. _reference-linux-mariadb-instalacion_mariadb:

###################
Instalación MariaDB
###################

En Fedora 20+, MySQL Workbench no esta en los repositorios, tampoco he probado Workbench
con MariaDB 10+ en ningún sistema.

Fedora
******

.. code-block:: bash

    yum -y install mariadb mariadb-server

    # Opcional
    yum -y install mysql-workbench

    systemctl start mariadb.service
    systemctl enable mariadb.service
    mysql_secure_installation

Ubuntu
******

En Ubuntu, hay que instalarlo con los repos de MariaDB:

* https://downloads.mariadb.org/mariadb/repositories/#mirror=cnrs

.. code-block:: bash

    sudo apt-get install software-properties-common
    sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
    sudo add-apt-repository 'deb http://ams2.mirrors.digitalocean.com/mariadb/repo/10.1/ubuntu trusty main'

    sudo apt-get update
    sudo apt-get install mariadb-server

    # Opcional
    apt-get install mysql-workbench

Ejecutar, para eliminar usuario temporal, etc

.. code-block:: bash

    mysql_secure_installation

    /etc/init.d/mysql restart

Crear un usuario y una database
*******************************

.. code-block:: bash

    mysql -u root -p
    CREATE USER snicoper@localhost IDENTIFIED BY '123456';
    CREATE DATABASE practicas;
    GRANT ALL ON practicas.* TO snicoper@localhost;
