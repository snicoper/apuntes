.. _reference-programacion-python-django-marcar_active_navbar_pagina_actual_en_templates:

########################################
Marcar active pagina actual en templates
########################################

Crear en la app **core** un directorio ``template_tags`` con su ``__init__.py``. Crear el archivo
``core_tags.py`` y añadir:

.. code-block:: python

    from django.template import Library
    from django.urls import reverse

    register = Library()


    @register.simple_tag
    def active_link(request, urlconf_name):
        """Devolvera active si request.path coincide con
        reverse(urlconf_name), en caso contrario devolvera ''.
        """
        url_reverse = reverse(urlconf_name)
        if request.path == url_reverse:
            return 'active'
        return ''

Para usarlo en el template, en el link que se quiere comprobar:

.. code-block:: html

    <li class="{% active_link request 'home_page' %}">
      <a href="{% url 'home_page' %}">Home</a>
    </li>

Nombre de la **tag** ``active_link``, el objeto ``request`` y el nombre en ``URLConf`` completo,
igual que se hace en un link ``{% url 'home:index' %}``.
