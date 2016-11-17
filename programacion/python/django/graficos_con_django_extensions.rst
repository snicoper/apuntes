.. _reference-programacion-python-django-graficos_con_django_extensions:

#################################################
Generar gráficos del modelo con django-extensions
#################################################

Para crear una representación gráfica de lo modelos, hay que tener instalado django-extensions.

Prerequisitos
*************

Se ha de instalar el paquete ``graphviz``, en Fedora:

.. code-block:: bash

    sudo dnf install graphviz graphviz-devel

Ahora en el entorno virtual (por ejemplo), instalar ``django-extensions`` y ``pygraphviz``.

.. code-block:: bash

    (my_venv) pip install django-extensions pygraphviz

Añadimos ``django-extensions`` en ``INSTALLED_APPS``.

.. code-block:: bash

    # my_project/settings.py

    INSTALLED_APPS = (
    # ...

    'django-extensions',
    )

Ahora, para generar las imágenes, de todos los modelos, incluidos los propios de Django:

.. code-block:: bash

    ./manage.py graph_models -a -o myapp_models.png

Y para generar de modelos específicos:

.. code-block:: bash

    ./manage.py graph_models myapp1 myapp2 > models.dot
    dot -Tpng models.dot -o models.png
