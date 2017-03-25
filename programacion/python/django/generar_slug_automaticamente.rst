.. _reference-programacion-python-django-generar_slug_automaticamente:

###############################
Generar un slug automaticamente
###############################

Con django

.. code-block:: python

    # myapp/models.py
    from django.db import models
    from django.template.defaultfilters import slugify
    from django.urls import reverse


    class Noticia(models.Model):
        titulo = models.CharField(max_length=200)
        slug = models.CharField(max_length=200, blank=True)

        def save(self, *args, **kwargs):
            self.slug = slugify(self.titulo)
            super(Noticia, self).save(*args, **kwargs)

Manualmente

.. code-block:: python

    # myapp/models.py
    import re

    from django.db import models
    from django.urls import reverse


    class Noticia(models.Model):
        titulo = models.CharField(max_length=200)
        slug = models.CharField(max_length=200, blank=True)

        def save(self, *args, **kwargs):
            self.slug = re.sub(r'[^a-z0-9+]', '-', self.titulo.lower())
            super(Noticia, self).save(*args, **kwargs)


https://docs.djangoproject.com/en/1.7/ref/contrib/admin/#django.contrib.admin.ModelAdmin.prepopulated_fields

.. code-block:: python

    # myapp/admin.py
    from django.contrib import admin

    from .models import Noticia

    class NoticiaAdmin(admin.ModelAdmin):
        prepopulated_fields = {'slug': ('titulo',)}


    admin.site.register(Noticia, NoticiaAdmin)
