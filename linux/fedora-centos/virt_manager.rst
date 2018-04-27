.. _reference-linux-fedora-centos-virt_manager:

############
Virt-Manager
############

Fuentes
*******

* http://fedoraproject.org/wiki/Getting_started_with_virtualization/es
* http://www.cyberciti.biz/faq/linux-kvm-stop-start-guest-virtual-machine/
* http://pic.dhe.ibm.com/infocenter/lnxinfo/v3r0m0/index.jsp?topic=%2Fliaat%2Fliaatkvmvirsh.htm

-------------------

.. code-block:: bash

    dnf install @virtualization

Ver :ref:`reference-linux-fedora-centos-reglas_selinux`

.. code-block:: bash

    systemctl enable libvirtd.service

.. important::
    Reiniar el equipo

Como usuario normal, crear una maquina virtual

.. code-block:: bash

    virt-install --name ns2.workspace.local --ram 1024 \
        --file=/home/snicoper/kvm/ns2.workspace.local.img \
        --file-size=8 --vnc \
        --cdrom=/run/media/snicoper/data/snicoper/Distros_Linux/CentOS-6.4-x86_64-bin-DVD1to2/CentOS-6.4-x86_64-bin-DVD1.iso

O bien

.. code-block:: bash

    virt-install --prompt

    Nombre de la maquina: ns2.workspace.local
    Ram utilizada (en megas): 1024
    Path donde guardara la maquina: /home/snicoper/kvm/ns2.workspace.local.img
    Disco duro en Gigas para la maquina: 8
    Path de la imagen iso: /ruta/imagen.iso

Algunos comandos
****************

Listar VMS funcionando
======================

.. code-block:: bash

    virsh list

Apagar Guest
============

.. code-block:: bash

    virsh list
    virsh shutdown Name
    virsh shutdown Id

Reiniciar Guest
===============

.. code-block:: bash

    virsh list
    virsh reboot Name
    virsh reboot Id

Forzar apagado
==============

.. code-block:: bash

    virsh list
    virsh destroy Name
    virsh destroy Id

Obtener información sobre un Guest
==================================

.. code-block:: bash

    virsh list
    virsh dominfo Name
    virsh dominfo Id

Obtener información sobre el nodo
=================================

.. code-block:: bash

    virsh nodeinfo

Eliminar una maquina
====================

Este lo hice a mano por que no me funciono.

.. code-block:: bash

    virsh destroy ns2.workspace.local
    virsh undefine ns2.workspace.local
    virsh vol-delete --pool vg0 ns2.workspace.local.img

Iniciar la maquina
==================

.. code-block:: bash

    virsh start ns2.workspace.local

Mostrarla
=========

.. code-block:: bash

    virt-viewer ns2.workspace.local
