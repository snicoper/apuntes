.. _reference-programacion-postgresql-crear_database_psql:

##############
Crear Database
##############

Para crear una base de datos y poner como propietario a alguien:

.. note::
    :ref:`reference-programacion-postgresql-crear_usuario_psql`

.. code-block:: sql

    sudo -u postgres psql postgres
    CREATE DATABASE practicas WITH OWNER snicoper;
