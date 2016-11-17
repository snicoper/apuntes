.. _reference-programacion-mariadb-recuperar_password_root:

#######################
Recuperar password root
#######################

Fuentes
*******

* http://www.guatewireless.org/os/linux/mysql-recuperar-la-contrasena-de-root-en-5-pasos/

--------

.. code-block:: bash

    /etc/init.d/mysql stop
    mysqld_safe --skip-grant-tables &
    mysql -u root
    use mysql;
    update user set password=PASSWORD("contraseña") where User='root';
    flush privileges;
    quit
    /etc/init.d/mysql stop
    /etc/init.d/mysql start
    mysql -u root -p
