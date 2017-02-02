.. _reference-programacion-postgresql-reset_sequence_id:

#################
Reset Sequence ID
#################

Ejecutar ``pg_dump`` primero para no meter la pata.

Se se han añadido y eliminado muchos campos y luego se quiere recuperar la secuencia del campo ``id`` en postgres.

.. code-block:: sql

    SELECT setval('table_name_id_seq', (SELECT MAX(id) FROM table_name));

Si se ha vaciado toda una tabla y se quiere resetear

.. code-block:: sql

    ALTER SEQUENCE table_name_id_seq RESTART;
