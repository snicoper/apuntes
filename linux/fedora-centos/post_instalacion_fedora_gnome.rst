.. _reference-linux-fedora-centos-post_instalacion_fedora_gnome:

#############################
Post instalación Fedora Gnome
#############################

**Fedora 39 Workstation**

:ref:`reference-linux-fedora-centos-post_instalacion_fedora`

Desinstalar
***********

.. code-block:: bash

    sudo dnf remove -y rhythmbox

Programas básicos
*****************

.. code-block:: bash

    sudo dnf -y install \
        dconf-editor \
        gnome-extensions-app \
        gnome-tweak-tool \
        gparted \
        transmission-gtk

Firewalld
*********

Poner por defecto ``zone=public`` y añadir la red local a ``trusted``

.. code-block:: bash

    sudo firewall-cmd --set-default-zone=public
    sudo firewall-cmd --permanent --zone=trusted --add-source=192.168.1.0/24
    sudo firewall-cmd --reload
