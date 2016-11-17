.. _reference-linux-mysql-instalacion_mysql_ubuntu:

########################
Instalación MySQL Ubuntu
########################

.. code-block:: bash

    sudo apt-get install mysql-server
    sudo mysql_secure_installation


Crear un usuario y una database
*******************************

.. code-block:: bash

    mysql -u root -p
    CREATE USER snicoper@localhost IDENTIFIED BY '123456';
    CREATE DATABASE practicas;
    GRANT ALL ON practicas.* TO snicoper@localhost;
