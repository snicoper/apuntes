.. _reference-linux-php-instalacion_laravel:

###################
Instalación Laravel
###################

**Fuentes**

* http://laravel.com/docs/quick#installation

-------

Fedora
======

.. code-block:: bash

    yum install -y php-curl

Centos 7, si se ha instalado php 5.5
====================================

.. code-block:: bash

    yum install --enablerepo=remi,remi-php55 php-curl

Ubuntu
======

.. code-block:: bash

    sudo apt-get install php5-curl

Composer o Archivo Phar
=======================

Creo que composer lo tiene mas actualizado ``composer self-update``,
con archivo Phar, has de estar descargándolo a "mano" cada que se quiera actualizar.

Composer
********

:ref:`reference-linux-php-composer`

.. code-block:: bash

    composer create-project laravel/laravel your-project-name --prefer-dist

Phar
====

Como root

.. code-block:: bash

    wget http://laravel.com/laravel.phar
    chmod +x laravel.phar
    mv laravel.phar /usr/local/bin/laravel
    laravel --version
