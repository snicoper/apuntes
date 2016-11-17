.. _reference-programacion-python-django-dumpload_data:

###################
loaddata y dumpdata
###################

**Fuentes**

* https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata

-------------

loaddata
********

.. code-block:: bash

    ./manage.py loaddata filename.json

dumpdata
********

Toda la base de datos

.. code-block:: bash

    ./manage.py dumpdata > db.json


Una app especifica

.. code-block:: bash

    ./manage.py dumpdata admin > admin.json

Una tabla especifica

.. code-block:: bash

    ./manage.py dumpdata auth.user > user.json

Indentacion en el archivo

.. code-block:: bash

    ./manage.py dumpdata auth.user --indent 2 > user.json