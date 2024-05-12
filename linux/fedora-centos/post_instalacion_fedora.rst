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

Descargar `Meslo.zip`` de https://github.com/ryanoasis/nerd-fonts/releases/download/v2.0.0/Meslo.zip

.. code-block:: bash

    cp *.ttf ~/.local/share/fonts/

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

Nvidia drivers
**************

.. code-block:: bash

    sudo dnf install xorg-x11-drv-nvidia-cuda
    sudo dnf install akmod-nvidia


Otras configuraciones
*********************

* :ref:`reference-linux-fedora-centos-post_instalacion_fedora_kde`
* :ref:`reference-linux-python-instalacion_python_fedora`
* :ref:`reference-programacion-python-apuntes_pip`
* :ref:`reference-linux-dotnet-instalacion_fedora_centos`
* :ref:`reference-linux-fedora-centos-podman`
* :ref:`reference-linux-fedora-centos-postfix`
* :ref:`reference-linux-instalacion_nodejs`
* :ref:`reference-linux-python-pip_upgrade_all_packages`
* :ref:`reference-linux-contar_lineas_proyecto`
