.. _reference-linux-fedora-centos-post_instalacion_fedora_gnome:

#############################
Post instalacion Fedora Gnome
#############################

**Fedora 25 Workstation**

:ref:`reference-linux-fedora-centos-post_instalacion_fedora`

Gnome Settings
**************

.. code-block:: bash

    # General
    gsettings set org.gnome.desktop.interface clock-show-date true
    gsettings set org.gnome.desktop.interface gtk-theme 'Adwaita-dark'
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

    # Files
    gsettings set org.gnome.nautilus.icon-view default-zoom-level 'standard'
    gsettings set org.gnome.nautilus.list-view use-tree-view true
    gsettings set org.gnome.nautilus.preferences default-folder-viewer 'icon-view'

    # Fuentes
    gsettings set org.gnome.desktop.interface monospace-font-name 'Dejavu Sans Mono 11'
    gsettings set org.gnome.settings-daemon.plugins.xsettings antialiasing 'rgba'
    gsettings set org.gnome.settings-daemon.plugins.xsettings hinting 'slight'

Global Dark Theme
*****************

.. code-block:: bash

    cat >> ~/.config/gtk-3.0/settings.ini << EOF
    [Settings]
    gtk-application-prefer-dark-theme=1
    EOF

**Firefox**

.. code-block:: bash

    vi ~/.profile

    # Añadir
    export MOZ_ALLOW_GTK_DARK_THEME=true

Require reloguear.

Terminix
********

.. code-block:: bash

    dnf copr enable heikoada/terminix

    dnf install -y terminix terminix-nautilus

Desinstalar
***********

.. code-block:: bash

    dnf remove -y \
        rhythmbox \
        evolution \
        shotwell

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        dconf-editor \
        geary \
        gnome-tweak-tool \
        gparted \
        gpick \
        transmission-gtk \
        yumex-dnf

Firewalld
*********

Poner por defecto ``zone=public`` y añadir la red local a ``trusted``

.. code-block:: bash

    firewall-cmd --set-default-zone=public
    firewall-cmd --zone=public --list-ports
    firewall-cmd --permanent --zone=trusted --add-source=192.168.1.0/24
    firewall-cmd --reload
    firewall-cmd --zone=trusted --list-sources
