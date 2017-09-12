.. _reference-linux-chromium-espanol:

######################
Chromium español Linux
######################

.. code-block:: bash

    sudo vim /usr/bin/chromium-browser

Añadir al inicio, después de ``#!/bin/bash``

.. code-block:: bash

    export LANGUAGE=es

Lo malo es que hay que hacerlo cada vez que se actualiza chromium.
