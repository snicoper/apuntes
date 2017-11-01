.. _reference-linux-fedora-centos-gnome_folder_colors:

###################
Gnome folder colors
###################

**Fuentes**

* https://ask.fedoraproject.org/en/question/65229/install-folder-color-in-fedora-20/

--------------

Forma 1
=======

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

Forma 2
=======

* https://launchpad.net/ubuntu/+source/folder-color/0.0.86-0ubuntu1

[Descargar](https://launchpad.net/ubuntu/+source/folder-color/0.0.86-0ubuntu1)
el ``.tar.gz`` y descomprimir.

.. code-block:: bash

    sudo cp ./folder-color_0.0.86.orig/nautilus/nautilus-extension/folder-color.py /usr/share/nautilus-python/extensions/folder-color.py
    nautilus -q
