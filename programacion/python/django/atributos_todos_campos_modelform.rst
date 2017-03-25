.. _reference-programacion-python-django-atributos_todos_campos_modelform:

#######################################################
Insertar atributos en todos los campos en un ModelForm
#######################################################

Para poder insertar un atributo en todos los campos de un formulario, por ejemplo
el ``class="form-control"`` y no estar haciéndolo de uno a uno en todos sus campos.

.. code-block:: python

    from django import forms

    from .models import IceCreamStore

    class IceCreamStoreForm(forms.ModelForm):

        class Meta:
            model = IceCreamStore

        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            for field in self.fields:
                # Recorremos todos los campos del modelo para añadirle class="form-control
                self.fields[field].widget.attrs.update({'class': 'form-control'})

            # Añadir atributos personalizados a un campo.
            self.fields['title'].widget.attrs.update({'placeholder': 'Titulo'})
