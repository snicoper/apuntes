.. _reference-linux-fedora-centos-post_instalacion_fedora:

#######################
Post instalacion Fedora
#######################

**Fedora 25 Workstation**

Gnome Settings
**************

.. code-block:: bash

    # General
    gsettings set org.gnome.desktop.interface clock-show-date true
    gsettings set org.gnome.desktop.interface gtk-theme 'Adwaita'
    gsettings set org.gnome.desktop.screensaver lock-enabled false
    gsettings set org.gnome.desktop.session idle-delay 900
    gsettings set org.gnome.desktop.wm.preferences button-layout 'appmenu:minimize,close'

    # Gedit
    gsettings set org.gnome.gedit.preferences.editor auto-indent true
    gsettings set org.gnome.gedit.preferences.editor bracket-matching true
    gsettings set org.gnome.gedit.preferences.editor highlight-current-line true
    gsettings set org.gnome.gedit.preferences.editor insert-spaces true
    gsettings set org.gnome.gedit.preferences.editor scheme 'solarized-dark'
    gsettings set org.gnome.gedit.preferences.editor tabs-size 4
    gsettings set org.gnome.gedit.preferences.editor wrap-last-split-mode 'word'
    gsettings set org.gnome.gedit.preferences.editor wrap-mode 'none'

    # Desktop
    gsettings set org.gnome.desktop.background show-desktop-icons true
    gsettings set org.gnome.nautilus.desktop home-icon-visible true
    gsettings set org.gnome.nautilus.desktop network-icon-visible false
    gsettings set org.gnome.nautilus.desktop trash-icon-visible false
    gsettings set org.gnome.nautilus.desktop volumes-visible false

    # Nautilus
    gsettings set org.gnome.nautilus.icon-view default-zoom-level 'standard'
    gsettings set org.gnome.nautilus.list-view use-tree-view true
    gsettings set org.gnome.nautilus.preferences default-folder-viewer 'icon-view'

    # Fuentes
    gsettings set org.gnome.desktop.interface monospace-font-name 'Dejavu Sans Mono 11'
    gsettings set org.gnome.settings-daemon.plugins.xsettings antialiasing 'rgba'
    gsettings set org.gnome.settings-daemon.plugins.xsettings hinting 'slight'

    # Otros
    gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

Terminix
********

.. code-block:: bash

    dnf copr enable heikoada/terminix

    dnf install -y terminix terminix-nautilus

Global Dark Theme
*****************

.. code-block:: bash

    cat >> ~/.config/gtk-3.0/settings.ini << EOF
    [Settings]
    gtk-application-prefer-dark-theme=1
    EOF

Eliminar algunos
****************

.. code-block:: bash

    dnf remove -y \
        rhythmbox \
        evolution \
        shotwell

Actualizar
**********

.. code-block:: bash

    dnf update -y

RPMFusion
*********

* http://rpmfusion.org/Configuration

.. code-block:: bash

    dnf install -y https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-25.noarch.rpm
    dnf install -y https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-25.noarch.rpm
    dnf update -y

Codecs
******

.. code-block:: bash

    dnf -y install \
        gstreamer-plugins-bad \
        gstreamer-plugins-bad-free-extras \
        gstreamer-plugins-bad-nonfree gstreamer-plugins-ugly \
        gstreamer-ffmpeg \
        gstreamer1-libav \
        gstreamer1-plugins-bad-free-extras \
        gstreamer1-plugins-bad-freeworld \
        gstreamer1-plugins-base-tools \
        gstreamer1-plugins-good-extras \
        gstreamer1-plugins-ugly \
        gstreamer1-plugins-bad-free \
        gstreamer1-plugins-good \
        gstreamer1-plugins-base \
        gstreamer1

Flash Player
************

.. code-block:: bash

    ## Adobe Repository 64-bit x86_64 ##
    rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
    dnf install -y flash-plugin

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        adobe-source-code-pro-fonts \
        cloc \
        cpp \
        ctags \
        ctags-etags \
        dconf-editor \
        dia \
        gcc \
        gcc-c++ \
        geary \
        gimp \
        git \
        gitg \
        gparted \
        gpick \
        htop \
        hunspell-es \
        kernel-devel \
        kernel-headers \
        make \
        meld \
        mutt \
        nmap \
        p7zip \
        p7zip-plugins \
        pwgen \
        transmission-gtk \
        unrar \
        vim \
        wget \
        yumex-dnf

Para pwgen ``pwgen -sy 16``

Opcionales
**********

.. code-block:: bash

    # Otros
    dnf -y install java-1.8.0-openjdk-devel
    dnf -y install adobe-source-code-pro-fonts
    dnf -y install levien-inconsolata-fonts
    dnf -y install gnome-tweak-tool
    dnf -y install zsh
    dnf -y install breeze-icon-theme
    dnf -y install gedit-plugins
    dnf -y install gnome-builder
    dnf -y install gnome-calendar
    dnf -y install gnome-music
    dnf -y install gnome-photos
    dnf -y install gnome-todo
    dnf -y install gnome-terminal-nautilus
    dnf -y install inkscape

Firewalld
*********

Poner por defecto ``zone=public`` y añadir la red local a ``trusted``

.. code-block:: bash

    firewall-cmd --set-default-zone=public
    firewall-cmd --zone=public --list-ports
    firewall-cmd --permanent --zone=trusted --add-source=192.168.1.0/24
    firewall-cmd --reload
    firewall-cmd --zone=trusted --list-sources

Idiomas
*******

.. code-block:: bash

    vim /etc/locale.conf

    LANG=en_US.UTF-8
    LC_NUMERIC=es_ES.UTF-8
    LC_TIME=es_ES.UTF-8
    LC_MONETARY=es_ES.UTF-8
    LC_PAPER=es_ES.UTF-8
    LC_MEASUREMENT=es_ES.UTF-8
    LC_CTYPE=es_ES.UTF-8
    LC_COLLATE=en_US.UTF-8
    LC_MESSAGES=en_US.UTF-8
    LC_NAME=es_ES.UTF-8
    LC_ADDRESS=es_ES.UTF-8
    LC_TELEPHONE=es_ES.UTF-8
    LC_IDENTIFICATION=es_ES.UTF-8

Post post instalación
*********************

* :ref:`reference-linux-python-instalacion_python_fedora`
* :ref:`reference-linux-postgresql-instalacion_postgresql`
* :ref:`reference-linux-postgresql-instalacion_postgis`
* :ref:`reference-programacion-python-apuntes_pip`
* :ref:`reference-linux-fedora-centos-postfix`
* :ref:`reference-linux-instalacion_nodejs`
* :ref:`reference-linux-python-pip_upgrade_all_packages`
* :ref:`reference-linux-contar_lineas_proyecto`
* :ref:`reference-linux-chromium-espanol`
