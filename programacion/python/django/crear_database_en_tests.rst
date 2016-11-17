.. _reference-programacion-python-django-crear_database_en_tests:

#########################
Permiso crear db en tests
#########################

Simplemente, el usuario ha de tener permisos para poder crear bases de datos.

En postgres:

.. code-block:: sql

    ALTER USER snicoper CREATEDB;
