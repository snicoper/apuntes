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
        kwrite \
        transmission-qt
