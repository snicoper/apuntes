.. _reference-programacion-python-django-settings_a_nivel_app:

###############################
Archivo settings a nivel de APP
###############################

Hay varias formas para tener configuraciones a nivel de aplicación.

# Opción 1

Crear archivo ``settings.py`` en la **app**

.. code-block:: python

    from django.conf import settings

    MI_CONFIGURACION = getattr(settings, 'MI_CONFIGURACION', 'valor por defecto')

Si no existe ``MI_CONFIGURACION`` en ``django.conf.settings`` le asigna un valor por defecto.

# Opción 2

Crear archivo ``settings.py``

.. code-block:: python

    from django.conf import settings as default_settings


    class AppSettings(object):

        def __setattr__(self, key, value):
            if key != key.upper():
                raise KeyError
            self.__dict__[key] = getattr(default_settings, key, value)

    settings = AppSettings()

    settings.MI_CONFIGURACION = 'valor por defecto'

``AppSettings`` podría estar en un archivo mas global a nivel de proyecto, por ejemplo en
``utils/default_settings.py``

.. code-block:: python

    from django.conf import settings as default_settings


    class AppSettings(object):

        def __setattr__(self, key, value):
            if key != key.upper():
                raise KeyError
            self.__dict__[key] = getattr(default_settings, key, value)

    settings = AppSettings()

Y luego a nivel de aplicación en el archivo ``settings.py``

.. code-block:: python

    from utils.default_settings import settings

    settings.MI_CONFIGURACION = 'Mi valor por defecto'

En todos los casos, para usarlo desde un archivo ``*.py``

.. code-block:: python

    from .conf import settings as myapp_settings

    print(myapp_settings.MI_CONFIGURACION)

Si ``MI_CONFIGURACION`` tiene un valor en ``settings.py`` (archivo de configuración por defecto de Django)
devolverá el valor de ``settings.MI_CONFIGURACION``, en caso contrario, ``app.settings.MI_CONFIGURACION``
