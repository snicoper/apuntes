.. _reference-linux-comando_dd:

##########
Comando dd
##########

Grabar de una .iso a un cd/pen

.. code-block:: bash

    sudo dd if=Fedora-14-x86_64-Live-KDE.iso of=/dev/sdb

Para crear una .iso de un cd/dvd

.. code-block:: bash

    dd if=/dev/lectora of=/home/usuario/Escritorio/dvd.iso
