.. _reference-programacion-python-apuntes_pip:

###########
Apuntes PIP
###########

psycopg2
********

.. code-block:: bash

    dnf install postgresql-devel

    (virtualenv) pip install psycopg2

Pillow
******

    | **Fuente**
    | http://pillow.readthedocs.org/en/latest/installation.html

.. code-block:: bash

    dnf install -y \
        libtiff-devel \
        libjpeg-devel \
        zlib-devel \
        freetype-devel \
        lcms2-devel \
        libwebp-devel \
        tcl-devel \
        tk-devel

pygraphviz
**********

Útil para generar gráficos de los modelos con `django-extensions <https://github.com/django-extensions/django-extensions>`_

.. code-block:: bash

    dnf install -y graphviz graphviz-devel

    (virtualenv) pip install pygraphviz
