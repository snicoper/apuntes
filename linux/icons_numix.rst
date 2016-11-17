.. _reference-linux-icons_numix:

############
Iconos Numix
############

.. code-block:: bash

    mkdir ~/souces
    cd ~/sources

    git clone https://github.com/numixproject/numix-icon-theme.git
    git clone https://github.com/numixproject/numix-icon-theme-circle.git

    mkdir ~/.local/share/icons
    cd ~/.local/share/icons

    ln -s ~/sources/numix-icon-theme/Numix Numix
    ln -s ~/sources/numix-icon-theme/Numix-Light Numix-Light
    ln -s ~/sources/numix-icon-theme-circle/Numix-Circle Numix-Circle
    ln -s ~/sources/numix-icon-theme-circle/Numix-Circle-Light Numix-Circle-Light
