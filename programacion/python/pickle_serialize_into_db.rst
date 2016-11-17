.. _reference-programacion-python-pickle_serialize_into_db:

#########################
Pickle serialize database
#########################

Serializa datos y los guarda en una base de datos.

Base de datos para el ejemplo

.. code-block:: sql

    CREATE TABLE datas
    (
      id serial NOT NULL,
      data_serializada text NOT NULL,
      CONSTRAINT pk_id_datas PRIMARY KEY (id)
    )

Ejemplo serializando un único objeto

.. code-block:: python

    import pickle
    import psycopg2

    conn_string = 'dbname=practicas \
                    user=snicoper \
                    password=123456'


    class Persona(object):

        def __init__(self, nombre, apellidos, email):
            self.nombre = nombre
            self.apellidos = apellidos
            self.email = email

    persona = Persona('salvador', 'nicolas pereiro', 'snicoper@example.com')

    # Guardar los datos en la db, pasar de bytes a str
    data = pickle.dumps(persona, 0)
    data = data.decode('utf-8')
    with psycopg2.connect(conn_string) as conn:
        with conn.cursor() as cur:
            cur.execute(
                "INSERT INTO datas(data_serializada) \
                VALUES(%s)", (data,))
            conn.commit()

    # Leer los datos
    with psycopg2.connect(conn_string) as conn:
        with conn.cursor() as cur:
            cur.execute(
                "SELECT * FROM datas WHERE id = 1")
            datas = cur.fetchone()

    # pasar de str a bytes
    datas = datas[1].encode('utf-8')
    p = pickle.loads(datas)
    print(p.nombre)

Ejemplo serializando varios objetos a la vez

.. code-block:: python

    persona = Persona('salvador', 'nicolas pereiro', 'snicoper@example.com')
    persona2 = Persona('perico', 'palote', 'perico@example.com')

    # Guardar los datos en la db, pasar de bytes a str
    data = pickle.dumps((persona, persona2), 0)
    data = data.decode('utf-8')
    with psycopg2.connect(conn_string) as conn:
        with conn.cursor() as cur:
            cur.execute(
                "INSERT INTO datas(data_serializada) \
                VALUES(%s) RETURNING id", (data,))
            conn.commit()
            last_id = cur.fetchone()[0]

    # Leer los datos
    with psycopg2.connect(conn_string) as conn:
        with conn.cursor() as cur:
            cur.execute(
                "SELECT * FROM datas \
                WHERE id=%s", (last_id,))
            datas = cur.fetchone()

    # pasar de str a bytes
    datas = datas[1].encode('utf-8')
    p1, p2 = pickle.loads(datas)
    print(type(p2))
