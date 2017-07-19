Django y MSSQL
**************

**Fuentes**

* https://github.com/michiya/django-pyodbc-azure

------------

Probado con sqlexpress 2016, python 3.6.1 x64, Windows 10 x64

.. code-block:: bash

    pip install django-pyodbc-azure

Configuración ``settings.py``

.. code-block:: python

    DATABASES = {
        'default': {
            'ENGINE': 'sql_server.pyodbc',
            'NAME': 'DbName',
            'USER': 'sa',
            'PASSWORD': 'PASSWORD',
            'HOST': 'DESKTOP-XXXXXXX\SQLEXPRESS',
            'OPTIONS': {
                'driver': 'ODBC Driver 13 for SQL Server'
            },
        }
    }

# Reverse Db

.. code-block:: bash

    python manage.py inspectdb
    python manage.py inspectdb > myapp/models.py
