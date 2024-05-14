.. _reference-linux-fedora-centos-post_instalacion_fedora:

#######################
Post instalación Fedora
#######################

**Fedora 40**

Actualizar
**********

.. code-block:: bash

    sudo dnf update -y

.. code-block:: bash

    sudo hostnamectl --static set-hostname ns1.snicoper.local

Codecs
******

.. code-block:: bash

    sudo dnf install \
        gstreamer1-plugins-{bad-\*,good-\*,base} \
        gstreamer1-plugin-openh264 gstreamer1-libav \
        --exclude=gstreamer1-plugins-bad-free-devel

    sudo dnf install lame\* --exclude=lame-devel

    sudo dnf group upgrade --with-optional Multimedia

Programas básicos
*****************

.. code-block:: bash

    sudo dnf -y install \
        cmake \
        cpp \
        dejavu-sans-mono-fonts \
        gcc \
        gcc-c++ \
        google-chrome-stable \
        git \
        hunspell-es \
        jetbrains-mono-fonts \
        kernel-devel \
        kernel-headers \
        p7zip \
        p7zip-plugins \
        powerline \
        powerline-fonts \
        unrar \
        vim \
        wget \
        zsh

Fuentes
*******

https://monaspace.githubnext.com/

- Descargar `Meslo.zip`` de https://github.com/ryanoasis/nerd-fonts/releases/download/v2.0.0/Meslo.zip

.. code-block:: bash

    mkdir -p ~/.local/share/fonts/
    cp *.otf ~/.local/share/fonts/

Idiomas
*******

.. code-block:: bash

    sudo vim /etc/locale.conf

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
    echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null

    sudo dnf install code -y

flatpak
*******

https://flathub.org/

.. code-block:: bash

    flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

    # Gnome extensions.
    flatpak install flathub org.gnome.Extensions

    # Github Desktop.
    flatpak install flathub io.github.shiftey.Desktop

    # Jetbrains Rider
    flatpak install flathub com.jetbrains.Rider

    # Dbeaver
    flatpak install flathub io.dbeaver.DBeaverCommunity

    # Google Chrome
    flatpak install flathub com.google.Chrome

    # Postman
    flatpak install flathub com.getpostman.Postman


Postman error al hacer login
****************************

.. code-block:: bash

    cd ~/.var/app/com.getpostman.Postman/config/Postman/proxy

    openssl req -subj '/C=US/CN=Postman Proxy' -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout postman-proxy-ca.key -out postman-proxy-ca.crt
