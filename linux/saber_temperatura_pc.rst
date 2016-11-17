.. _reference-linux-saber_temperatura_pc:

########################
Saber temperatura del PC
########################

**Fuentes**

* http://blog.desdelinux.net/sensors-conoce-todas-las-temperaturas-de-tu-ordenador/

------

.. code-block:: bash

    sudo apt-get install lm-sensors

La terminal te puede mostrar la temperatura en tiempo real con tan solo poner:

.. code-block:: bash

    watch -n 01 sensors
