.. _reference-linux-montar_particiones_al_iniciar_sistema:

#####################################
Montar particiones al iniciar sistema
#####################################

.. note::
    Ver las particiones que se quiere montar con ``fdisk -l``
    o ``df``

Fedora ntfs
***********

Desmontar partición (si esta montada) y crear directorio data

.. code-block:: bash

    su
    umount /run/media/snicoper/data
    mkdir -p /run/media/snicoper/data

.. code-block:: bash

    vim /etc/fstab

Insertar al final

.. code-block:: bash

    ### data
    /dev/sda6 /run/media/snicoper/data ntfs defaults,rw,users,auto,iocharset=utf8,umask=0

Montar particiones

.. code-block:: bash

    mount -a

Ubuntu ntfs
***********

.. code-block:: bash

    sudo umount /run/media/snicoper/data
    mkdir -p /run/media/snicoper/data

.. code-block:: bash

    vim /etc/fstab

.. code-block:: bash

    /dev/sda5 /run/media/snicoper/data ntfs defaults,rw,users,auto,iocharset=utf8,umask=0

.. code-block:: bash

    mount -a

Fedora ext4
***********

.. code-block:: bash

    mkdir -p /run/media/snicoper/data

.. code-block:: bash

    vim /etc/fstab

.. code-block:: bash

    /dev/sda3 /run/media/snicoper/data auto nosuid,nodev,nofail,x-gvfs-show,x-gvfs-name=data 1 2

Si es la primera vez que se crea la partición, crear un directorio

.. code-block:: bash

    mkdir /run/media/snicoper/data
    chown snicoper:snicoper /run/media/snicoper/data

Fedora btrfs
************

.. code-block:: bash

    /dev/sdaX /run/media/snicoper/data btrfs defaults,user,auto 0 2
