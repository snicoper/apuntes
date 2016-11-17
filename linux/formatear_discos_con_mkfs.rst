.. _reference-linux-formatear_discos_con_mkfs:

#########################
Formatear discos con mkfs
#########################

.. caution::
    Cuidado con estos comando que pueden ser peligrosos,
    asegurarse de poner bien las particiones con las que
    se quiere operar.

Desmontar la partición

.. code-block:: bash

    umount /dev/sdb?

FAT
***
.. code-block:: bash

    mkfs.vfat /dev/sdb1 # Lo deja en fat-16?
    mkfs.vfat -n pen4 -F 32 /dev/sdb1 # -n para label

Ext2, 3, 4
***********

.. code-block:: bash

    mkfs -t ext? /dev/sdb?

Swap
****

.. code-block:: bash

    mkswap /dev/sdb?

btrfs

.. code-block:: bash

    mkfs.btrfs -f /dev/sdb?

Poner label en una partición

.. code-block:: bash

    e2label /dev/sda5 nombre_label
