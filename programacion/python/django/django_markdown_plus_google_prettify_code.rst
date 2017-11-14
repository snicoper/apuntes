.. _reference-programacion-python-django-django_markdown_plus_google_prettify_code:

#################################
Django Markdown y Google Prettify
#################################

**TODO:** Cambiar esto por **highlightjs** y simplemente :ref:`reference-programacion-python-django-django_markdown`

**Fuentes**

* https://github.com/timmyomahony/django-pagedown
* https://github.com/trentm/django-markdown-deux
* https://code.google.com/p/google-code-prettify/wiki/GettingStarted

--------------------

Una manera rápida para añadir entradas con ``markdown`` y/o resaltar bloques
de código.

Mientras que ``django-pagedown`` lo uso para mostrar el <textarea> con algunos
botones de ayuda para formatear el código markdown, ``django-markdown-deux``
lo utilizo la presentación (formateado).

Y por ultimo, utilizo ``google-code-prettify`` para el resaltado de sintaxis.

Instalación:

.. code-block:: bash

    pip install django-pagedown
    pip install django-markdown-deux

Añadir en ``settings.py``

.. code-block:: python

    INSTALLED_APPS = (
        # [...]
        'markdown_deux',
        'pagedown',
    )

django-pagedown
***************

Todos los ``TextField`` de un modelo.

Añadir en ``admin.py``:

.. code-block:: python

    from django.contrib import admin
    from django.db import models

    from pagedown.widgets import AdminPagedownWidget

    from .models import Article


    class ArticleAdmin(admin.ModelAdmin):
        formfield_overrides = {
            models.TextField: {'widget': AdminPagedownWidget},
        }

    admin.site.register(Article, ArticleAdmin)

Ver todas las opciones `django-pagedown <https://github.com/timmyomahony/django-pagedown>`_

django-markdown-deux
********************

Para la presentación y formateo de marcado.

Añado en el template que mostrara el código markdown

.. code-block:: html

    {% extends 'base.html' %}
    {% load markdown_deux_tags %}

    {% block content %}
      <h2>{{ article.title }}</h2><hr>
      <div>
        {{ article.body|markdown }}
      </div>
    {% endblock content %}

Ver todas las opciones `django-markdown-deux <https://github.com/trentm/django-markdown-deux>`_

google-code-prettify
********************

Descargar y descomprimir ``prettify-small-4-Mar-2013.tar.bz2`` o la versión
mas reciente.

Renombro ``google-code-prettify`` a ``prettify`` y la pego en
``project_dajngo/static/js/``.

Entro dentro de ``project_dajngo/static/js/prettify/``, corto ``prettify.css`` y pego
en ``project_dajngo/static/css/``.

Añado en la parte del ``css``.

.. code-block:: htmldjango

    <link href="{% static "css/prettify.css" %}" rel="stylesheet">

y en la parte del javascript.

.. code-block:: htmldjango

    <script src="{% static "js/prettify/prettify.js" %}"></script>
    <script type='text/javascript'>
          $('pre').addClass('prettyprint');
          prettyPrint();
    </script>

**Algunos themes para prettify**

* http://demo.stanleyhlng.com/prettify-js/?id=bootstrap-light
* http://jmblog.github.io/color-themes-for-google-code-prettify/


Scroll si el código es muy largo, en el archivo ``.css``

.. code-block:: css

    pre code {
        overflow: auto;
        display: block;
        line-height: 1.6em;
        white-space: pre;
        word-wrap: normal;
        /* Si se quiere poner un height maximo */
        /*max-height: 600px;*/
    }

Números en las lineas, modificar ``$('pre').addClass('prettyprint');`` por
``$('pre').addClass('prettyprint linenums');``

Otra opción para el resaltado de sintaxis `highlight.js <https://highlightjs.org/>`_
