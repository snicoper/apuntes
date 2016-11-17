.. _reference-linux-instalacion_memcached:

########################
Instalación de Memcached
########################

Fedora
******

.. code-block:: bash

    yum -y install memcached

    systemctl enable memcached.service
    systemctl start memcached.service

Para editar la configuración

.. code-block:: bash

    vim /etc/sysconfig/memcached

Ubuntu
******

.. code-block:: bash

    sudo apt-get install memcached libmemcached-tools

Para editar la configuración

.. code-block:: bash

    sudo vim /etc/memcached.conf

