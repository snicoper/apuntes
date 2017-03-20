.. _reference-linux-fedora-centos-copr:

#################
Repositorios Copr
#################

Algunos repos de ``copr``

Neovim
******

* https://copr.fedorainfracloud.org/coprs/dperson/neovim/

.. code-block:: bash

    dnf copr -y enable dperson/neovim
    dnf update -y
    dnf install -y neovim

terminix
********

* https://github.com/gnunn1/terminix#install-terminix

.. code-block:: bash

    dnf copr enable heikoada/terminix
    dnf update -y
    dnf install -y terminix

Atom
****

* https://copr.fedorainfracloud.org/coprs/mosquito/atom/

.. code-block:: bash

    dnf copr enable mosquito/atom
    dnf update -y
    dnf install -y atom

La Capitaine Icon Theme
***********************

.. code-block:: bash

    dnf copr enable tcg/themes
    dnf install la-capitaine-icon-theme

    # Como usuario normal.
    gsettings set org.gnome.desktop.interface icon-theme 'La Capitaine'