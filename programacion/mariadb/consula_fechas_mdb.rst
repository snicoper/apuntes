.. _reference-programacion-mariadb-consula_fechas_mdb:

###############
Consulta fechas
###############

Consultas básicas de MySQL

Comparar fechas, por ejemplo buscar usuarios que han nacido en un mes actual

.. code-block:: sql

    SELECT *
    FROM usuarios
    WHERE MONTH(fecha_nacimiento) = MONTH(CURDATE());

Con ``CURDATE()`` o ``NOW()`` dentro de ``MONTH(), DAYOFMONTH(), YEAR()``, etc, compara
una fecha pasada con la fecha actual.

El libro de MySQL de Paul Dubois en la pagina 90+ muestra ejemplos de fechas.
