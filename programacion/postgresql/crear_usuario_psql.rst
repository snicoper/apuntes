.. _reference-programacion-postgresql-crear_usuario_psql:

##########
Crear User
##########

Para crear un usuario:

.. note::
    :ref:`reference-programacion-postgresql-crear_database_psql`

.. code-block:: sql

    sudo -u postgres psql postgres
    CREATE USER snicoper WITH PASSWORD '123456' NOCREATEDB NOCREATEUSER;
