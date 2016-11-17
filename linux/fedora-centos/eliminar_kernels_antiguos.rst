.. _reference-linux-fedora-centos-eliminar_kernels_antiguos:

########################
Eliminar Kernel Antiguos
########################

.. danger::
    Cuidado de no eliminar el que se esta usando, nunca me ha pasado, pero no
    se si lo permitiria.

Fuentes
*******
http://my.opera.com/man666/blog/quitar-kernels-antiguos-en-fedora

------------

Como usuario root, para ver todos los kernels instalados

.. code-block:: bash

    rpm -qa | grep kernel-

Para eliminar el o los kernels viejos

.. code-block:: bash

    rpm -e kernel-2.6.38.2-9.fc15.x86_64
