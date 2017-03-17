.. _reference-programacion-python-django-reset_migrations:

################
Reset migrations
################

Mientras el proyecto esta en desarrollo y aun no esta en producción, es mas fácil,
simplemente con este comando desde root del proyecto.

.. code-block:: bash

    # Eliminar todos los archivos de migraciones, excepto __init__.py
    find . -path "*/migrations/*.py" -not -name "__init__.py" -delete

    # Generar el 0001_initial.py en cada app con directorio migrations.
    ./manage.py makemigrations

    # migrate fake.
    ./manage.py migrate --fake

**Nota:** con ``django-boilerplate``:

.. code-block:: bash

    delete_migrations.sh
    ./manage.py makemigrations
    ./manage.py migrate --fake

En desarrollo, **probar primero en desarrollo.**, los comandos anteriores,
actualizar los archivos den ``prod`` (``git pull prod``)

.. code-block:: bash

    # django-boilerplate.
    ./prod_manage.py migrate --fake

    # django con settings de producción.
    ./manage.py migrate --fake --settings=production_settings

Esto ya hace los cambios en la tabla ``django_migrations``
