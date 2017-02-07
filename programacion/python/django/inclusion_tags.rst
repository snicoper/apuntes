.. _reference-programacion-python-django-inclusion_tags:

#####################################
Template tags y filter personalizados
#####################################

**Fuentes**

* https://docs.djangoproject.com/es/1.10/howto/custom-template-tags/

----

A veces, va bien crear plantillas base que importan datos y mostrarlos, por ejemplo
un menú lateral con categorías, pero que solo es útil para la app X.

Para no estar mandando esos mismos datos desde las vistas a los templates desde
todas las vista, una manera mas rápida y sencilla, es creándolas con
``template tags``.

Para el ejemplo, tenemos un modelo muy simple.

.. code-block:: python

    class Category(models.Model):

        name = models.CharField(max_length=254)
        # [...]

La platilla ``blog/_categories.html``

.. code-block:: html

    <ul>
        {% for cat in categories %}
            <li>{{ cat.name }}</li>
        {% endfor %}
    </ul>

Dentro de la ``app`` creamos un directorio con el nombre ``templatetags`` y
dentro de ``templatetags`` un archivo ``__init__.py`` y por ultimo
un archivo donde irán los template tags con el nombre ``blog_tags``.

.. code-block:: python

    from django import template

    from ..models import Category

    register = template.Library()


    @register.inclusion_tag('blog/_categories.html')
    def get_category_list():
        return {'categories': Category.objects.all()}

Y ahora, cada vez que queramos mostrar (importar), el trozo de código
de ``blog/_categories.html``, tendremos que hacer uso de ``load``
en cualquier ``template`` de nuestro sitio.

.. code-block:: html

    <!-- Añadir load antes de llamar a get_category_list -->
    {% load blog_tags %}

    <!-- Y ahora, en la parte que se necesite blog/_categories.html  -->
    {% get_category_list %}

También es posible pasar parámetros, para verlos, mirar las fuentes.

Crear un archivo en ``templatetags`` con un nombre ``form_helper_tags`` o similar e introducir:

.. code-block:: python

    import re

    from django import template
    from django.utils.safestring import mark_safe

    register = template.Library()


    @register.filter
    def add(html_input, properties):
        """
        Inserta propiedades en un campo html.

        Uso: {{ form.field_name|add:'class="form-control" placeholder="Placeholder here"' }}
        """
        pattern = r'(\s\/>|>)'
        regex = re.compile(pattern, re.IGNORECASE)
        replace = ' {0}>'.format(properties)
        html = regex.sub(replace, str(html_input))
        return mark_safe(html)

Para usar, desde el template html

.. code-block:: python

    {% load form_helper_tags %}

    # ...
    <div class="form-group">
        {{ form.field_name.label_tag }}
        {{ form.field_name|add:'class="form-control" placeholder="Placeholder here"' }}
    </div>
    # ...
