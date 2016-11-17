.. _reference-programacion-python-django-municipios_espana:

########################################
Municipios de España en la base de datos
########################################

**Fuentes:**

* http://www.ine.es/jaxi/menu.do?type=pcaxis&path=%2Ft20%2Fe245%2Fcodmun%2F&file=inebase&L=0
* https://iagolast.wordpress.com/2014/11/23/creando-un-select-ajax-de-provincias-y-municipios-espanoles/

Desde la pagina de http://www.ine.es se puede acceder Comunidades autónomas, provincias y municipios.
El mas laborioso sin duda son los municipios, que son mas de 8000 en toda España.

Las comunidades autónomas y provincias, las hago a mano, respetando los códigos como clave primaria.

Para generar **fixtures** con Django, descargo el archivo **Fichero con todas las provincias** /
**Relación de municipios por provincia e isla**

Después ejecuto el siguiente código, que es una modificación de https://iagolast.wordpress.com

Es necesario instalar ``pip install xlrd``

.. code-block:: python

    import xlrd
    import json


    def xls_to_json(filename):
        doc = xlrd.open_workbook(filename)
        sheet = doc.sheet_by_index(0)
        nrows = sheet.nrows
        municipios = []
        pk = 0

        if not is_valid(sheet):
            print("Error en {0}, el archivo tiene un formato inesperado.".format(filename))

        for row in range(3, nrows):
            pk += 1
            cod_mun = sheet.cell_value(row, 0)
            name_mun = sheet.cell_value(row, 3)

            municipios.append(
                {'model': 'poblaciones.municipio', 'pk': pk, 'fields': {
                    'name': name_mun,
                    'provincia': cod_mun
                }}
            )
        with open('initial_data.json', 'wb') as fp:
            json_string = json.dumps(municipios, ensure_ascii=False).encode('utf8')
            fp.write(json_string)


    def is_valid(sheet):
        if str(sheet.cell_value(1, 0)) != "CPRO":
            print("Se esperaba CPRO y se tiene {0}".format(sheet.cell_value(2, 0)))
            return False
        if str(sheet.cell_value(1, 1)) != "CMUN":
            print("Se esperaba CMUN y se tiene {0}".format(sheet.cell_value(2, 1)))
            return False
        if str(sheet.cell_value(1, 2)) != "DC":
            print("Se esperaba DC y se tiene {0}".format(sheet.cell_value(2, 2)))
            return False
        if str(sheet.cell_value(1, 3)) != "NOMBRE":
            print("Se esperaba NOMBRE y se tiene {0}".format(sheet.cell_value(2, 3)))
            return False
        return True

    xls_to_json('15codmun.xls')


Después ejecutarlo con ``./manage.py loaddata initial_data``

.. note::

    Es necesario tener una tabla con los campos ``name`` y ``provincia``, donde provincia es la id
    de la tabla ``provincias``

.. code-block:: python

    class Municipio(models.Model):
        """Municipios."""

        name = models.CharField(max_length=255)
        provincia = models.ForeignKey(Provincia, related_name='municipio_provincia')
