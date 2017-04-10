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

la-capitaine-icon-theme
***********************

* https://github.com/keeferrourke/la-capitaine-icon-theme

.. code-block:: bash

    dnf copr enable tcg/themes
    dnf install la-capitaine-icon-theme

    gsettings set org.gnome.desktop.interface icon-theme 'La Capitaine'
