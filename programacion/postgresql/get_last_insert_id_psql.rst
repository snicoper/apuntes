.. _reference-programacion-postgresql-get_last_insert_id_psql:

####################################
Obtener ultimo ID insertado en la db
####################################

.. code-block:: sql

    INSERT INTO persons (lastname,firstname) VALUES ('Smith', 'John') RETURNING id

Ejeplo con Python

.. code-block:: python

    with psycopg2.connect(conn_string) as conn:
        with conn.cursor() as cur:
            cur.execute(
                "INSERT INTO persons(lastname, firstname) \
                VALUES(%s, %s) RETURNING id", (firstname, lastname))
            conn.commit()
            print(cur.fetchone()[0])
