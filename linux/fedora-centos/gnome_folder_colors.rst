.. _reference-linux-fedora-centos-gnome_folder_colors:

###################
Gnome folder colors
###################

**Fuentes**

* https://ask.fedoraproject.org/en/question/65229/install-folder-color-in-fedora-20/

--------------

Ir a http://rpm.pbone.net/index.php3/ y buscar ``folder-color``

Descargar:

* ``folder-color-common-X.X.XX-X.X.noarch.rpm``
* ``folder-color-nautilus-X.X.XX-X.X.noarch.rpm``

.. code-block:: bash

    cd directorio/descargas
    sudo rpm -ivh --nodeps \
        folder-color-common-X.X.XX-X.X.noarch.rpm \
        folder-color-nautilus-X.X.XX-X.X.noarch.rpm

Reiniciar o 'relogear'.
