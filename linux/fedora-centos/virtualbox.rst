.. _reference-linux-fedora-centos-virtualbox:

##########
Virtualbox
##########

Fuentes
*******

* http://www.if-not-true-then-false.com/2010/install-virtualbox-with-yum-on-fedora-centos-red-hat-rhel/

---------------

Para versiones Fedora < 22 o Centos, ver el enlace de **Fuentes**, aquí solo me pongo la de Fedora (22)

.. code-block:: bash

    # Repo
    cd /etc/yum.repos.d/
    wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo

    # Actualizar
    dnf update

    # Dependencias
    dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms

    # Instalar
    dnf install VirtualBox-5.0

    # Inicializar
    # /etc/init.d/vboxdrv setup
    /usr/lib/virtualbox/vboxdrv.sh setup

    # Dar permisos a usuario
    usermod -a -G vboxusers snicoper
