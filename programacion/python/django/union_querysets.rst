.. _reference-programacion-python-django-union_querysets:

##################
Union de QuerySets
##################

**Fuentes**

* http://stackoverflow.com/questions/431628/how-to-combine-2-or-more-querysets-in-a-django-view
* http://stackoverflow.com/questions/15596497/django-multiple-queryset-combine-into-a-pagination

-----------

Obtener las consultas.

.. code-block:: python

    c1 = MyModel1.objects.all()
    c2 = MyModel2.objects.all()
    c3 = MyModel3.objects.all()

Unirlos con ``chain``:

.. code-block:: python

    from itertools import chain

    result_list = list(chain(c1, c2, c3))

    # Si se quiere ordenar por algun campo.
    result_list = sorted(
        chain(c1, c1, c3),
        key=attrgetter('create_at')
    )

Con el operados de union ``|`` (siguiendo con ``c1``, ``c2`` y ``c3``)

.. code-block:: python

    result_list c1 | c2 | c3

El "problema" es que han ser del mismo modelo.

En el comentario también habla de ``QuerySetChain`` en
