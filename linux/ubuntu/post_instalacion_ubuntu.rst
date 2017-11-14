.. _reference-linux-ubuntu-post_instalacion_ubuntu:

#######################
Post instalación Ubuntu
#######################

**Probado en Ubuntu 14.04**

-----------------

Si se usa **Calligra**, eliminar **LibreOffice** antes de actualizar.

.. code-block:: bash

    sudo apt remove --purge libreoffice*

Actualizar.

.. code-block:: bash

    sudo apt update && sudo apt dist-upgrade

Si es una instalación de VirtualBox.

.. code-block:: bash

    sudo apt install virtualbox-guest-dkms

Instalar Vim.

.. code-block:: bash

    sudo apt -y install vim

Cambiar editor.

.. code-block:: bash

    sudo update-alternatives --config editor

Programas básicos.

.. code-block:: bash

    sudo apt install -y \
        build-essential \
        git \
        git-cola \
        exuberant-ctags \
        curl \
        wget \
        ssh \
        unrar \
        htop \
        nmap \
        tree \
        python-pygments

    # JDK y JRE
    sudo apt install -y \
        openjdk-7-jre \
        openjdk-7-jdk

Diccionario español.

.. code-block:: bash

    sudo apt install aspell-es myspell-es -y

KDE
===

Si se configura Akonadi con SQLite o PostgreSQL.

Cambiar en Menú > buscar ``Akonadi Server Configuration``.

.. code-block:: bash

    sudo apt install akonadi-backend-sqlite
    sudo apt install akonadi-backend-postgresql

Muon.

.. code-block:: bash

    sudo apt -y install muon

Calligra.

.. code-block:: bash

    sudo apt install calligra -y

kdiff3.

.. code-block:: bash

    sudo apt install kdiff3-qt -y

Utilidades KDE.

.. code-block:: bash

    sudo apt install kgpg kleopatra kcolorchooser -y

Para visualizar las miniaturas en Dolphin de los .pdf.

.. code-block:: bash

    sudo apt install kdegraphics-thumbnailers -y

Eliminar.

.. code-block:: bash

    sudo apt remove --purge kget amarok -y

Opcionales.

.. code-block:: bash

    sudo apt install kdeplasma-addons -y

Transmision.

.. code-block:: bash

    sudo apt install transmission-qt -y

qBittorent.

.. code-block:: bash

    sudo apt install qbittorrent -y

-----------------------

GNOME
=====

Eliminar en Ubuntu Unity Amazon.

.. code-block:: bash

    sudo apt remove --purge unity-webapps-common

Synaptic.

.. code-block:: bash

    sudo apt install synaptic

Open terminal here.

.. code-block:: bash

    sudo apt install nautilus-open-terminal

Meld.

.. code-block:: bash

    sudo apt install meld -y

gpick.

.. code-block:: bash

    sudo apt install gpick -y

LibreOffice.

.. code-block:: bash

    sudo apt install libreoffice

RabbitVCS.

.. code-block:: bash

    sudo add-apt-repository ppa:rabbitvcs/ppa
    sudo apt update
    sudo apt install rabbitvcs-nautilus3 rabbitvcs-cli

Menus have icons y buttons have icons

.. code-block:: bash

    gsettings set org.gnome.desktop.interface menus-have-icons true
    gsettings set org.gnome.desktop.interface buttons-have-icons true

-------------------

KDE/GNOME
================

Umbrello.

.. code-block:: bash

    sudo apt install -y  umbrello

Gui SQLite.

.. code-block:: bash

    sudo apt install -y sqlitebrowser

Thunderbird.

.. code-block:: bash

    sudo apt install thunderbird

Chromium.

.. code-block:: bash

    sudo apt install chromium-browser -y

Vlc.

.. code-block:: bash

    sudo apt install vlc

Inskape y gimp.

.. code-block:: bash

    sudo apt install gimp inkscape

Filezilla.

.. code-block:: bash

    sudo apt install filezilla

Kdevelop.

.. code-block:: bash

    sudo apt install kdevelop cmake

kdevelop python.

.. code-block:: bash

    sudo apt install kdev-python pep8

qtcreator.

.. code-block:: bash

    sudo apt -y install qtcreator

No mostrar la opción de cuenta de invitado al hacer login.

.. code-block:: bash

    sudo sh -c 'printf "[SeatDefaults]\nallow-guest=false\n" >/usr/share/lightdm/lightdm.conf.d/50-no-guest.conf'
