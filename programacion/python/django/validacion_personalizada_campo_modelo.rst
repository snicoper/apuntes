.. _reference-programacion-python-django-validacion_personalizada_campo_modelo:

#############################
Validación campo de un modelo
#############################

.. code-block:: python

    # my_app/validators.py

    from django.core.exceptions import ValidationError


    def titulo_validation(value):
        if not len(value) > 4:
            raise ValidationError('Mínimo 4 caracteres')

.. code-block:: python

    # my_app/models.py

    from django.db import models

    from .validators import titulo_validation


    class Articulo(models.Model):
        titulo = models.CharField(max_length=200, validators=[titulo_validation])

        #....

Tambien es posible hacerlo desde un ``ModelForm``

.. code-block:: python

    # my_app/forms.py

    from django import forms

    from .models import Articulo
    from .validators import titulo_validation

    class MyForm(models.ModelForm):

        def __init__(self):
            super().__init__(*args, **kwargs)
            self.fields['titulo'].validators.append(titulo_validation)

        class Meta:
            model = Articulo
