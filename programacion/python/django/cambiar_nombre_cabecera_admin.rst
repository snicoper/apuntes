.. _reference-programacion-python-django-cambiar_nombre_cabecera_admin:

#####################################################
Cambiar el nombre en la cabecera de la administración
#####################################################

El el **URLConf** principal ``myproject/urls.py`` añadir

.. code-block:: python

    from django.conf.urls import include, url
    from django.contrib import admin

    urlpatterns = [
        url(r'^admin/', include(admin.site.urls)),
    ]

    # Añadir
    admin.site.site_header = 'Nuevo nombre'
