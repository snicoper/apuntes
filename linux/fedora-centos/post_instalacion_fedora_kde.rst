.. _reference-linux-fedora-centos-post_instalacion_fedora_kde:

###########################
Post instalación Fedora KDE
###########################

**Fedora 25 KDE**

:ref:`reference-linux-fedora-centos-post_instalacion_fedora`

Desinstalar
***********

.. code-block:: bash

    dnf remove -y \
        akregator \
        amarok \
        kate \
        kdegames-minimal \
        kget \
        knode \
        konqueror \
        ktorrent \
        qupzilla

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        ffmpegthumbs \
        kwrite \
        transmission-qt

``ffmpegthumbs`` Previews para los videos en Dolphin, se ha de activar igual que las imágenes.

Firewalld
*********

Añadir la red local a ``trusted``

.. code-block:: bash

    firewall-cmd --permanent --zone=trusted --add-source=192.168.1.0/24
    firewall-cmd --reload
