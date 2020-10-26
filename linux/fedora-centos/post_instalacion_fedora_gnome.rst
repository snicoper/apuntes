.. _reference-linux-fedora-centos-post_instalacion_fedora_gnome:

#############################
Post instalación Fedora Gnome
#############################

**Fedora 33 Workstation**

:ref:`reference-linux-fedora-centos-post_instalacion_fedora`

Desinstalar
***********

.. code-block:: bash

    dnf remove -y \
        gnome-terminal-nautilus \
        rhythmbox

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        gnome-tweak-tool \
        gparted \
        tilix \
        tilix-nautilus \
        transmission-gtk

Si nautilus no muestra ``Open Tilix Here``

.. code-block:: bash

    dnf -y install python2-gobject
    nautilus -q

Firewalld
*********

Poner por defecto ``zone=public`` y añadir la red local a ``trusted``

.. code-block:: bash

    firewall-cmd --set-default-zone=public
    firewall-cmd --permanent --zone=trusted --add-source=192.168.1.0/24
    firewall-cmd --reload
