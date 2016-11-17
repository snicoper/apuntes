.. _reference-programacion-python-leer_guardar_datos_json_en_db_psql_python:

##################################
Leer y guardar datos json en la db
##################################

Leer y guardar datos JSON en una base de datos con psycopg2.

El ejemplo es muy simple, pero para una rápida referencia, lo guardo.

.. code-block:: python

    import json
    import psycopg2


    def connect():
        conn = psycopg2.connect(" \
            dbname=practicas \
            user=snicoper \
            password=123456")
        return conn


    def save_data(data):
        conn = connect()
        cursor = conn.cursor()
        cursor.execute('insert into datas(data) values(%s)', (data,))
        conn.commit()
        conn.close()


    def load_data(id):
        conn = connect()
        cursor = conn.cursor()
        cursor.execute('SELECT * FROM datas WHERE id = %s', (id, ))
        datos = cursor.fetchone()
        conn.close()
        return datos


    # Guardar en la db
    archivo_json = 'tests/datas.json'
    json_datas = open(archivo_json)
    data = json.load(json_datas)
    print(json.dumps(data))
    save_data(json.dumps(data))

    json_datas.close()

    # Leer desde la db
    datos = load_data(3)[1]
    datos_json = json.loads(datos)
    print(datos_json['nombre'])
