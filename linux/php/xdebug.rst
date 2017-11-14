.. _reference-linux-php-xdebug:

######
XDebug
######

Ver :ref:`reference-linux-php-instalacion_php`

Ubuntu
******

.. code-block:: bash

    sudo apt-get install php5-xdebug

    sudo vim /etc/php5/mods-available/xdebug.ini

.. code-block:: bash

    zend_extension=/usr/lib/php5/20100525/xdebug.so
    xdebug.remote_enable=on
    xdebug.remote_handler=dbgp
    xdebug.remote_host=localhost
    xdebug.remote_port=9000
    xdebug.output_buffering=off

Fedora
******

.. code-block:: bash

    dnf install php-pecl-xdebug -y

Centos PHP 5
************

.. code-block:: bash

    yum install --enablerepo=remi,remi-php55 php-pecl-xdebug

Fedora y Centos PHP 5
=====================

.. code-block:: bash

    vim /etc/php.d/xdebug.ini

.. code-block:: bash

    ; Enable xdebug extension module
    zend_extension=/usr/lib64/php/modules/xdebug.so
    xdebug.remote_enable=on
    xdebug.remote_handler=dbgp
    xdebug.remote_host=localhost
    xdebug.remote_port=9090
    xdebug.output_buffering=off
