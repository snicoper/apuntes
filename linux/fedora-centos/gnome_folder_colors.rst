.. _reference-linux-fedora-centos-gnome_folder_colors:

###################
Gnome folder colors
###################

* https://launchpad.net/ubuntu/+source/folder-color/0.0.86-0ubuntu1

`Descargar <https://launchpad.net/ubuntu/+source/folder-color/0.0.86-0ubuntu1>`_ el ``.tar.gz`` y descomprimir.

.. code-block:: bash

    # Usuario
    mkdir -p ~/.local/share/nautilus-python/extensions ~/.local/share/nautilus-python/extensions/folder-color.py
    cp folder-color_0.0.86.orig/nautilus/nautilus-extension/folder-color.py

    # Global
    sudo cp ./folder-color_0.0.86.orig/nautilus/nautilus-extension/folder-color.py /usr/share/nautilus-python/extensions/folder-color.py
    nautilus -q
