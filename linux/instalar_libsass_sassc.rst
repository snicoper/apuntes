.. _reference-linux-instalar_libsass_sassc:

########################
Instalar Libsass y SassC
########################

**Fuentes**

* http://crocodillon.com/blog/how-to-install-sassc-and-libsass-on-ubuntu

---

Pre Requisitos
**************

.. warning::

    TODO: Poner paquetes de compilación requeridos

.. code-block:: bash

    su -
    cd /usr/local/lib

    git clone https://github.com/hcatlin/sassc.git
    git clone https://github.com/hcatlin/libsass.git

Añadir ``SASS_LIBSASS_PATH`` al path para todos los usuarios.

.. code-block:: bash

    vim /etc/profile.d/sassc.sh

    export SASS_LIBSASS_PATH=/usr/local/lib/libsass

.. code-block:: bash

    source /etc/profile

.. code-block:: bash

    cd /usr/local/lib/sassc
    make
    chmod +x bin/sassc

.. code-block:: bash

    cd /usr/local/bin/
    ln -s ../lib/sassc/bin/sassc sassc
