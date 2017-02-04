.. _reference-linux-dropbox:

################
Instalar Dropbox
################

GNOME
*****

.. warning::
    Posiblemente des-actualizado

.. code-block:: bash

    su
    yum install -y wget

Addition yum repo file from Dropbox

.. code-block:: bash

    wget http://dl.dropbox.com/u/30876345/repo/dropbox.repo

.. code-block:: bash

    mv dropbox.repo /etc/yum.repos.d

Install Dropbox

.. code-block:: bash

    yum install -y nautilus-dropbox

KDE
***

.. code-block:: bash

    cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -

Autoarranque al iniciar en el sistema

.. code-block:: bash

    ln -s .dropbox-dist/dropboxd .kde/Autostart/dropboxd

Iniciar por primera vez

.. code-block:: bash

    ~/.dropbox-dist/dropboxd &

.. note::
    No recuerdo si había que ponerlo en inicio de sesión o no
