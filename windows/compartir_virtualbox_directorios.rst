.. _reference-windows-compartir_virtualbox_directorios:

###################################
Compartir directorios en VirtualBox
###################################

Todo esto esta pensado para tener como host a windows virtualizando linux.

En windows, virtualbox (Host)
*****************************

Entrar en la configuración de la maquina virtual de VB y en la opciones
de red pongo ``Adaptador puente``

En carpetas compartidas -> Carpetas de la máquina:

* Ruta carpeta: ``Ruta de la carpeta host``
* Nombre carpeta: ``Nombre para identificarlo``
* Sólo lectura: ``Desactivado``
* Automontar: ``Activado``
* Hacer permanente: ``Activado``

Linux, maquina virtualizada (Guest)
***********************************

**Requisitos**

* Tener instalado virtualbox-guest-additions.
* Tener uno o varios usuarios creados.

Añadir usuario/s al grupo ``vboxsf``

.. code-block:: bash

    sudo usermod -a -G vboxsf snicoper

reiniciar

Las carpetas se automontan en (ubuntu) ``/media/sf_Nombre_carpeta``

Ahora si se quiere tener mas a mano:

.. code-block:: bash

    ln -s /media/sf_Nombre_carpeta ~/nombre_carpeta

--------

Con Samba
*********

De esta manera, se puede compartir, por ejemplo, todo el directorio de un usuario linux
y acceder desde windows, como la carpeta entera de home.

Ubuntu
======

.. code-block:: bash

    sudo apt install samba
    sudo smbpasswd -a snicoper

    sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.copia

    vim /etc/samba/smb.conf

    # Añadir al final
    [home_snicoper]
    path = /home/snicoper
    available = yes
    valid users = snicoper
    read only = no
    browseable = yes
    public = yes
    writable = yes

    # Reiniciar samba
    sudo restart smbd

Fedora/Centos
=============

.. code-block:: bash

    yum install samba samba-client samba-common -y

    /usr/bin/smbpasswd -a snicoper


Editar ``smb.conf``

.. code-block:: bash

    cp /etc/samba/smb.conf /etc/samba/smb.conf.copia
    vim /etc/samba/smb.conf

    # Linea 66 añadir:
    unix charset = UTF-8

    # Linea 89 modificar:
    workgroup = WORKGROUP

    # Linea 95 descomentar y modificar:
    hosts allow = 127. 192.168.1.

    # Linea 125 añadir:
    map to guest = Bad User

    # Añadir al final:
    [home_snicoper]
    path = /home/snicoper
    writable = yes
    browsable = yes
    guest ok = yes
    guest only = yes
    create mode = 0777
    directory mode = 0777


**SELinux**

.. code-block:: bash

    setsebool -P samba_enable_home_dirs on

**Firewall**

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=samba
    firewall-cmd --reload

**Iniciar y añadir como servicio**

.. code-block:: bash

    systemctl start smb.service
    systemctl enable smb.service

Windows
=======

Ir a ``This PC`` y añadir Map network drive, seguir los pasos.

* Drive: Elegir una letra
* Folder: \\\\192.168.1.2\\snicoper
