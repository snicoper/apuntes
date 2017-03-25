.. _reference-programacion-python-django-django_markdown:

###############
Django markdown
###############

Este lo tengo mas actualizado https://github.com/snicoper/django-boilerplate/blob/master/src/apps/utils/templatetags/utils_tags.txt#L10

.. code-block:: bash

    pip install markdown2

Crear un template filter

.. code-block:: python

    # filters_tags.py
    import markdown2

    from django import template
    from django.utils.safestring import mark_safe


    @register.filter('markdown')
    def markdown_format(text):
        """Devuelve el texto markdown en HTML.

        Args:
            text str: Texto markdown
        Returns:
            str El markdown convertido en HTML.
        """
        return mark_safe(markdown2.markdown(text))

Desde un template .html

.. code-block:: html

    {% load filters_tags %}

    {{ article.body|markdown }}
