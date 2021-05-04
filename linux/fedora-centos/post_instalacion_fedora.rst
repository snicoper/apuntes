.. _reference-linux-fedora-centos-post_instalacion_fedora:

#######################
Post instalación Fedora
#######################

**Fedora 33**

Actualizar
**********

.. code-block:: bash

    dnf update -y

.. code-block:: bash

    sudo su -
    passwd root

    hostnamectl --static set-hostname ns1.snicoper.local

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
        compat-ffmpeg28 \
        gstreamer-plugins-bad \
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
        bashtop \
        cloc \
        cpp \
        ctags \
        ctags-etags \
        flameshot \
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
        powerline \
        powerline-fonts \
        pwgen \
        sqlite \
        sqlitebrowser \
        unrar \
        util-linux-user \
        vim \
        wget

Para pwgen ``pwgen -sy 16``

Git flow
********

* https://github.com/petervanderdoes/gitflow-avh

Otros
*****

.. code-block:: bash

    dnf -y install mediawriter
    dnf -y install zsh
    dnf -y install chromium
    dnf -y install discord
    dnf -y install levien-inconsolata-fonts
    dnf -y install telegram-desktop


.. code-block:: bash

    dnf config-manager --set-enabled google-chrome


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

    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    dnf install -y code

Otras configuraciones
*********************

* :ref:`reference-linux-fedora-centos-post_instalacion_fedora_kde`
* :ref:`reference-linux-python-instalacion_python_fedora`
* :ref:`reference-linux-postgresql-instalacion_postgresql`
* :ref:`reference-programacion-python-apuntes_pip`
* :ref:`reference-linux-dotnet-instalacion_fedora_centos`
* :ref:`reference-linux-fedora-centos-podman`
* :ref:`reference-linux-fedora-centos-postfix`
* :ref:`reference-linux-instalacion_nodejs`
* :ref:`reference-linux-python-pip_upgrade_all_packages`
* :ref:`reference-linux-contar_lineas_proyecto`
