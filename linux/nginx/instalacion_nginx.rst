.. _reference-linux-nginx-instalacion_nginx:

#################
Instalación Nginx
#################

Fedora
******

Instalación

.. code-block:: bash

    dnf install -y nginx

Centos
******

.. note::
    También están en los repos de remi
    :ref:`reference-linux-fedora-centos-post_instalacion_centos`

.. code-block:: bash

    vim /etc/yum.repos.d/nginx.repo

Añadir

.. code-block:: bash

    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
    gpgcheck=0
    enabled=1

.. code-block:: bash

    yum update
    yum install -y nginx

Fedora y Centos
===============

.. code-block:: bash

    systemctl start nginx.service
    systemctl enable nginx.service

Firewall

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --add-service=https
    firewall-cmd --reload

Si se crea un host en el home, se ha de dar permisos ``711`` al home del usuario

.. code-block:: bash

    chmod 711 /home/snicoper

Ver :ref:`reference-linux-fedora-centos-reglas_selinux`
