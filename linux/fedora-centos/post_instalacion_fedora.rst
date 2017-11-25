.. _reference-linux-fedora-centos-post_instalacion_fedora:

#######################
Post instalación Fedora
#######################

**Fedora 27**

Actualizar
**********

.. code-block:: bash

    dnf update -y

RPM Fusion
**********

* http://rpmfusion.org/Configuration

.. code-block:: bash

    dnf install -y https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
    dnf install -y https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
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

Programas básicos
*****************

.. code-block:: bash

    dnf -y install \
        adobe-source-code-pro-fonts \
        cloc \
        cpp \
        ctags \
        ctags-etags \
        gcc \
        gcc-c++ \
        git \
        htop \
        hunspell-es \
        kernel-devel \
        kernel-headers \
        make \
        mutt \
        p7zip \
        p7zip-plugins \
        pwgen \
        sqlite \
        tilix \
        tilix-nautilus \
        unrar \
        util-linux-user \
        vim \
        wget

Para pwgen ``pwgen -sy 16``

Otros
*****

.. code-block:: bash

    dnf -y install chromium
    dnf -y install gimp
    dnf -y install zsh
    dnf -y install meld
    dnf -y install gitg

    dnf -y install telegram-desktop

    dnf -y install gedit-plugins
    dnf -y install breeze-icon-theme
    dnf -y install dia
    dnf -y install gnome-todo
    dnf -y install gnome-builder
    dnf -y install gnome-calendar
    dnf -y install gnome-music
    dnf -y install gnome-photos
    dnf -y install gnome-terminal-nautilus # Si no se instala tilix.
    dnf -y install inkscape
    dnf -y install java-1.8.0-openjdk-devel
    dnf -y install krita
    dnf -y install levien-inconsolata-fonts
    dnf -y install umbrello

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

vscode
******

* https://code.visualstudio.com/docs/setup/linux

.. code-block:: bash

    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    sudo dnf install -y code

Atom
****

* https://fedoraproject.org/wiki/Atom

Instalar o Actualizar Atom

Editar ``~/.bashrc`` o ``~/.zshrc``.

.. code-block:: bash

    # Comprueba si Atom tiene la ultima version y la actualiza en caso necesario.
    # Si no esta instalado, lo instala.
    function atom_update() {
        ATOM_RPM="atom.x86_64.rpm"
        ATOM_INSTALLED_VERSION=$(rpm -qi atom | grep "Version" |  cut -d ':' -f 2 | cut -d ' ' -f 2)
        ATOM_LATEST_VERSION=$(curl -sL "https://api.github.com/repos/atom/atom/releases/latest" | grep -E "https.*atom-amd64.tar.gz" | cut -d '"' -f 4 | cut -d '/' -f 8 | sed 's/v//g')

        if [[ ! $ATOM_INSTALLED_VERSION ]]
        then
            wget https://github.com/atom/atom/releases/download/v${ATOM_LATEST_VERSION}/${ATOM_RPM}
            sudo dnf install -y $ATOM_RPM
            rm -rf $ATOM_RPM
        elif [[ $ATOM_INSTALLED_VERSION < $ATOM_LATEST_VERSION ]]
        then
            wget https://github.com/atom/atom/releases/download/v${ATOM_LATEST_VERSION}/${ATOM_RPM}
            sudo dnf install -y $ATOM_RPM
            rm -rf $ATOM_RPM
        else
            echo "Atom esta en la ultima versión"
        fi
    }

    alias atom_update="atom_update"

Otras configuraciones
*********************

* :ref:`reference-linux-fedora-centos-post_instalacion_fedora_gnome`
* :ref:`reference-linux-fedora-centos-post_instalacion_fedora_kde`
* :ref:`reference-linux-python-instalacion_python_fedora`
* :ref:`reference-linux-postgresql-instalacion_postgresql`
* :ref:`reference-linux-postgresql-instalacion_postgis`
* :ref:`reference-programacion-python-apuntes_pip`
* :ref:`reference-linux-fedora-centos-postfix`
* :ref:`reference-linux-instalacion_nodejs`
* :ref:`reference-linux-python-pip_upgrade_all_packages`
* :ref:`reference-linux-contar_lineas_proyecto`
* :ref:`reference-linux-chromium-espanol`
