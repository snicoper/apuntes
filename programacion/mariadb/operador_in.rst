.. _reference-programacion-mariadb-operador_in:

###########
Operador IN
###########

El operador IN() es util para cuando se buscan varios valores dentro de una
consulta.

La forma tradicional seria

.. code-block:: sql

    SELECT *
    FROM members
    WHERE id_member = '10'
    OR id_member = '20';

Lo que devolvería 2 usuarios, id 10 e id 20

Otra manera para hacerlo seria con IN()

.. code-block:: sql

    SELECT *
    FROM members
    WHERE id_member IN('10', '20');
