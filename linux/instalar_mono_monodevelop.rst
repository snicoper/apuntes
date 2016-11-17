.. _reference-linux-instalar_mono_monodevelop:

#############################
Instalar Mono Monodevelop Xsp
#############################

DESACTUALIZADO!

**Fuentes**

* http://www.mono-project.com/docs/getting-started/install/linux/

-------------------

Fedora Centos
*************

Añadir repo

.. code-block:: bash

    sudo rpm --import "https://pgp.mit.edu/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"

    # Fedora
    sudo dnf config-manager --add-repo http://download.mono-project.com/repo/centos/

    # Centos
    sudo yum-config-manager --add-repo http://download.mono-project.com/repo/centos/

**Instalar**

.. code-block:: bash

    # yum para centos
    sudo dnf install mono-complete xsp monodevelop

Ubuntu
*************

.. warning::
    No probado...

Añadir repo

.. code-block:: bash

    sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list

**Instalar**

.. code-block:: bash

    sudo apt install mono-complete xsp monodevelop

Ubuntu Fedora
*************

Como usuario:

.. code-block:: bash

    mozroots --import --sync

Por ultimo dar permisos.

.. code-block:: bash

    sudo mkdir -p /etc/mono/registry/LocalMachine
    sudo chmod g+rwx /etc/mono/registry
    sudo chmod g+rwx /etc/mono/registry/LocalMachine
