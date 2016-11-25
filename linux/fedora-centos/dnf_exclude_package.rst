.. _reference-linux-fedora-centos-dnf_exclude_package:

####################
DNF Exclude Packages
####################

Excluir un paquete al actualizar.

Desde la linea de comandos:

.. code-block:: bash

    dnf update --exclude=packagename

Editando ``/etc/dnf/dnf.conf``

.. code-block:: bash

    vim /etc/dnf/dnf.conf

    # Añadir
    exclude=packagename
