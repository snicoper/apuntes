.. _reference-linux-fedora-centos-copr:

#################
Repositorios Copr
#################

Nodejs
******

* https://copr.fedoraproject.org/coprs/nibbler/nodejs/

.. code-block:: bash

    # Versión LTS
    dnf copr -y enable nibbler/nodejs4

    # Ultima versión
    dnf copr -y enable nibbler/nodejs

    dnf update -y
    dnf install -y nodejs npm

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
