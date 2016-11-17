.. _reference-linux-fedora-centos-cambiar_plymouth:

################
Cambiar Plymouth
################

.. code-block:: bash

    yum install plymouth-theme-solar
    plymouth-set-default-theme solar
    dracut --force

    reboot

Para saber los themes que tenemos instalados.

.. code-block:: bash

    plymouth-set-default-theme -l
