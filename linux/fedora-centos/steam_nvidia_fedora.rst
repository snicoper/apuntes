.. _reference-linux-fedora-centos-steam_nvidia_fedora:

##############
Steam + Nvidia
##############

No probado
**********

.. code-block:: bash

    sudo dnf install akmod-nvidia
    sudo dnf install xorg-x11-drv-nvidia-cuda
    sudo dnf update -y

Probado en **Fedora 26 + GeForce GTX 650**
*******************************************

Requiere de **RPM Fusion**

.. code-block:: bash

    su -

    dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
    dnf install -y \
        nvidia-driver
        nvidia-driver-libs.i686
        steam

    reboot
