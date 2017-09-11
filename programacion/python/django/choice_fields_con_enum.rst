.. _reference-programacion-python-django-choice_fields_con_enum:

############################
Choice fields con class Enum
############################

**Fuentes**

* Two Scoops of Django 1.11 - Pag 78 - 6.4.8 Better Model Choice Constants Using Enum

---

.. code-block:: python

    from django import models
    from enum import Enum


    class IceCreamOrder(models.Model):

        class FLAVORS(Enum):
            chocolate = ('ch', 'Chocolate')
            vanilla = ('vn', 'Vanilla')
            strawberry = ('st', 'Strawberry')
            chunky_munky = ('cm', 'Chunky Munky')

            @classmethod
            def get_value(cls, member):
                return cls[member].value[0]

        flavor = models.CharField(
            max_length=2,
            choices=[x.value for x in FLAVORS]
        )


.. code-block:: bash

    >>> from orders.models import IceCreamOrder
    >>> chocolate = IceCreamOrder.FLAVORS.get_value('chocolate')
    >>> IceCreamOrder.objects.filter(flavor=chocolate)
    [<icecreamorder: 35>, <icecreamorder: 42>, <icecreamorder: 49>]

Incluso con un **mixin**

.. code-block:: python

    class EnumMixin(object):

        @classmethod
        def get_value(cls, member):
            return cls[member].value[0]

        # Otros methods...


    class IceCreamOrder(models.Model):

        class FLAVORS(EnumMixin, Enum):
            chocolate = ('ch', 'Chocolate')
            vanilla = ('vn', 'Vanilla')
            strawberry = ('st', 'Strawberry')
            chunky_munky = ('cm', 'Chunky Munky')
