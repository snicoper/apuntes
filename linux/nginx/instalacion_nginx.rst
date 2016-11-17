.. _reference-linux-nginx-instalacion_nginx:

#################
Instalación Nginx
#################

Ubuntu
******

Instalación

.. code-block:: bash

    sudo apt install nginx
    sudo service nginx start

Si se quiere permitir que puedan verse las paginas desde fuera del localhost
añadir regla en ufw

.. code-block:: bash

    sudo ufw allow 80

Ubuntu PPA
**********

* https://launchpad.net/~nginx/+archive/ubuntu/development
* http://wiki.nginx.org/Install

.. code-block:: bash

    sudo -s
    nginx=stable # use nginx=development for latest development version
    sudo add-apt-repository ppa:nginx/$nginx
    sudo apt-get update
    sudo apt-get install nginx

Fedora
******

Instalación

.. code-block:: bash

    dnf install -y nginx

Centos
******

.. note::
    Tambien estan en los repos de remi
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
