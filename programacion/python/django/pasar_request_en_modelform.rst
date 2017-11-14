.. _reference-programacion-python-django-pasar_request_en_modelform:

########################################################
Pasar request en un Form o ModelForm desde generic.*View
########################################################

En el ``FormView`` o lo que sea ``*View`` crear método:

.. code-block:: python

    class MyView(generic.FormView):

        def get_form_kwargs(self):
            kwargs = super().get_form_kwargs()
            kwargs['request'] = self.request
            return kwargs

Ahora estará accesible en el ``Form`` desde el método ``__init__()``.

.. code-block:: python

    class MyForm(forms.ModelForm):

        def __init__(self, *args, **kwargs):
            self.request = kwargs.pop('request', None)
            super().__init__(*args, **kwargs)
