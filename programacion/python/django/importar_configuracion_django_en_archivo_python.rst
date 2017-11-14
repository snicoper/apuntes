.. _reference-programacion-python-django-importar_configuracion_django_en_archivo_python:

###############################################
Importar configuración django en archivo python
###############################################

.. code-block:: python

    import os
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'nombre_proyecto.settings')

    import django
    django.setup()

    from my_app.models import MiModel1, MiModel2

    # ....
