.. _reference-programacion-python-optener_diccionario_de_consulta_sql:

#######################################
Obtener diccionario de una consulta sql
#######################################

**Fuentes**

* http://stackoverflow.com/questions/16519385/output-pyodbc-cursor-results-as-python-dictionary

-----

.. code-block:: python

    cursor = connection.cursor()
    cursor.execute(sql)
    columns = [column[0] for column in cursor.description]
    results = []
    for row in cursor.fetchall():
        results.append(dict(zip(columns, row)))
    print(results)

