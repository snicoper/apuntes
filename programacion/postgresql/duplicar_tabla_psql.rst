.. _reference-programacion-postgresql-duplicar_tabla_psql:

############################
Duplicar tabla en postgresql
############################

Fuentes
*******

* http://www.mkyong.com/database/postgresql-create-table-from-exisiting-table/

-----------

.. code-block:: sql

    CREATE TABLE 'nombre_nueva_tabla' AS SELECT 'tabla_a_copiar';

Si la tabla ``tabla_a_copiar`` esta poblada y no deseamos copiar los
datos existentes, se puede poner un ``WHERE`` en la consulta.

.. code-block:: sql

    CREATE TABLE 'nombre_nueva_tabla'
    AS SELECT 'tabla_a_copiar'
    WHERE 1 = 2;

Como 1 no es igual a 2, no se insertara ningún dato de la 1º tabla.
