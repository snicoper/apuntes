.. _reference-programacion-python-django-how_to_create_language_files:

#############################
Cómo crear archivos de idioma
#############################

**Fuentes**

* https://docs.djangoproject.com/en/dev/topics/i18n/translation/
* http://www.i18nguy.com/unicode/language-identifiers.html
* http://django-book.readthedocs.org/en/latest/chapter19.html

-------

Es posible hacerlo de dos maneras diferentes.

Desde la raíz del proyecto Django, donde esta ``manage.py`` o desde la raíz de la ``app``.

**Desde la raíz del proyecto**

Hay que editar ``settings.py`` para decirle los módulos que tendrán traducciones.

.. code-block:: python

    LOCALE_PATHS = (
        os.path.join(BASE_DIR, 'apps/home/locale/'),
    )

Requiere crear el directorio ``locale`` manualmente?

Después, ejecutar

.. code-block:: bash

    ./manage.py makemessages -l es

Donde ``es`` es el identificador de lenguaje, `aqui <http://www.i18nguy.com/unicode/language-identifiers.html>`_ una lista

**Desde la raíz de la app**

Aquí no es necesario añadir ``LOCALE_PATHS`` a ``settings.py``, y en vez de usar ``manage.py``, se
usa ``django-admin.py``, además el directorio locale se ha de crear a mano.

.. code-block:: bash

    cd myapp
    mkdir locale
    django-admin.py makemessages -l es

El script recorre completamente el árbol en el cual es ejecutado y extrae todas las cadenas marcadas
para traducción. Crea (o actualiza) un archivo de mensajes en el directorio ``locale``.
En el ejemplo ``es``, el archivo será ``locale/de/LC_MESSAGES/django.po``.

Dentro de los archivos ``.po``, se va algo así.

.. code-block:: python

    #: views.py:6
    msgid "name"
    msgstr "nombre"

* **msgid** es la cadena de traducción, la cual aparece en el código fuente. No la modifiques.
* **msgstr** es donde colocas la traducción específica a un idioma. Su valor inicial es vacío de manera que es tu responsabilidad el cambiar esto. Asegúrate de que mantienes las comillas alrededor de tu traducción.
* Por conveniencia, cada mensaje incluye el nombre del archivo y el número de línea desde el cual la cadena de traducción fue extraída.

.. code-block:: python

    #...
    from django.utils.translation import gettext as _


    def index(request):
        var_name = _('name')
    #...

el valor de ``var_name`` sera ``nombre``

Después, hay que compilarlo con ``compilemessages``, y se aplica lo mismo que antes, cuando se hizo
desde la raiz del proyecto Django o desde la raíz de la aplicación.

.. code-block:: bash

    # desde la raíz del proyecto
    ./manage.py compilemessages

    # desde la raíz de la aplicacion
    django-admin.py compilemessages

Para reexaminar todo el código fuente y las plantillas en búsqueda de nuevas cadenas de traducción y
actualizar todos los archivos de mensajes para todos los idiomas, ejecuta lo siguiente:

.. code-block:: bash

    ./manage.py/django-admin.py makemessages -a

**Algunas notas**

Para configurar una preferencia de idioma a nivel de la instalación, fija ``LANGUAGE_CODE`` en tu archivo
de configuración. Django usará este idioma como la traducción por omisión – la opción a seleccionarse
en último término si ningún otro traductor encuentra una traducción.

Si deseas permitir que cada usuario individual especifique el idioma que ella o él prefiere, usa
``LocaleMiddleware``. ``LocaleMiddleware`` permite la selección del idioma basado en datos incluidos
en la petición. Personaliza el contenido para cada usuario.

Para usar ``LocaleMiddleware``, agrega ``django.middleware.locale.LocaleMiddleware`` a tu
variable de configuración ``MIDDLEWARE_CLASSES``. Debido a que el orden de los middlewares es relevante, deberías seguir las siguientes guías:

* Asegúrate de que se encuentre entre las primeras clases middleware instaladas.
* Debe estar ubicado después de SessionMiddleware, esto es debido a que LocaleMiddleware usa datos de la sesión.
* Si usas CacheMiddleware, coloca LocaleMiddleware después de este (de otra forma los usuarios podrían recibir contenido cacheado del locale equivocado).

``LocaleMiddleware`` intenta determinar la preferencia de idioma del usuario siguiendo el siguiente
algoritmo:

* Primero, busca una clave ``django_language`` en la sesión del usuario actual.
* Se eso falla, busca una cookie llamada ``django_language``.
* Si eso falla, busca la cabecera HTTP ``Accept-Language``. Esta cabecera es enviada por tu nave- gador y le indica al servidor qué idioma(s) prefieres en orden de prioridad. Django intenta con cada idioma que aparezca en dicha cabecera hasta que encuentra uno para el que haya disponible una traducción.
* Si eso falla, usa la variable de configuración global ``LANGUAGE_CODE``.
