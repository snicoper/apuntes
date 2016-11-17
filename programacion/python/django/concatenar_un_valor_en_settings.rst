.. _reference-programacion-python-django-concatenar_un_valor_en_settings:

##################################
Concatenar un valor en settings.py
##################################

**Fuentes**

* http://stackoverflow.com/questions/2246725/django-template-context-processors

--------

Por ejemplo, para añadir en ``TEMPLATE_CONTEXT_PROCESSORS`` el request
``django.core.context_processors.request`` dentro de ``settings.py``

.. code-block:: python

    from django.conf import global_settings

    TEMPLATE_CONTEXT_PROCESSORS = global_settings.TEMPLATE_CONTEXT_PROCESSORS + (
        'django.core.context_processors.request',
    )
