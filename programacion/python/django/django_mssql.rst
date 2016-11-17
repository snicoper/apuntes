Django y MSSQL
**************

**Fuentes**

* https://django-mssql.readthedocs.org/en/latest/index.html
* https://bitbucket.org/Manfre/django-mssql
* http://sourceforge.net/projects/pywin32/

------------

Probado con sqlexpress 2014, python 3.4.2 x64, Windows 8.1


.. code-block:: bash

    pip install django-mssql

Descargar el .exe de `pywin32 <http://sourceforge.net/projects/pywin32/>`_
según versión y arquitectura

Yo lo instalo con virtualenv, supongo que si se hace en el python
principal, doble click, siguiente, siguiente...

.. code-block:: bash

    # Con virtualenv
    cd ~/Downloads
    easy_install pywin32-219.win-amd64-py3.4.exe

Configuración de settings.py

.. code-block:: python

    DATABASES = {
        'default': {
            'NAME': 'django',
            'ENGINE': 'sqlserver_ado',
            'HOST': r'.\SQLEXPRESS',
            'USER': 'snicoper',
            'PASSWORD': '123456',
            'OPTIONS': {
                'provider': 'SQLNCLI11',
            },
        }
    }
