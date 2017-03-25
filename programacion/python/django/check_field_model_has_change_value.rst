.. _reference-programacion-python-django-check_field_model_has_change_value:

##############################################
Comprobar si un campo de un modelo ha cambiado
##############################################

**Fuentes**

* http://stackoverflow.com/a/1793323

-----

.. code-block:: python

    class Person(models.Model):
        name = models.CharField()

        __original_name = None

        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.__original_name = self.name

        def save(self, force_insert=False, force_update=False, *args, **kwargs):
            if self.name != self.__original_name:
                # name changed - do something here

            super().save(force_insert, force_update, *args, **kwargs)
            self.__original_name = self.name
