.. _reference-linux-fedora-centos-copr:

#################
Repositorios Copr
#################

Algunos repos de ``copr``

Atom
****

* https://copr.fedorainfracloud.org/coprs/mosquito/atom/

.. code-block:: bash

    dnf copr enable mosquito/atom
    dnf install -y atom

La Capitaine Icon Theme
***********************

.. code-block:: bash

    dnf copr enable tcg/themes
    dnf install la-capitaine-icon-theme

    # Como usuario normal.
    gsettings set org.gnome.desktop.interface icon-theme 'La Capitaine'
