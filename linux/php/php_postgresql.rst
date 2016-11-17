.. _reference-linux-php-php_postgresql:

##############
PHP PostgreSQL
##############

Ubuntu
******

.. code-block:: bash

    sudo apt-get install -y php5-pgsql

    # Opcional
    sudo apt-get install -y phppgadmin

Configurar phppgadmin

.. code-block:: bash

    sudo vim /usr/share/phppgadmin/conf/config.inc.php

Buscar ``$conf['extra_login_security']`` y poner el valor a ``false``

.. code-block:: bash

    $conf['extra_login_security'] = false;

Fedora
******

.. code-block:: bash

    yum install -y php-pgsql

    # Opcional
    yum install -y phpPgAdmin

Centos
******

Para PHP 5.5

.. code-block:: bash

    yum install -y php-pgsql --enablerepo=remi,remi-php55

    # Opcional
    yum install -y phpPgAdmin --enablerepo=remi,remi-php55

Configuracon phpPgAdmin, Fedora y Centos
========================================

.. code-block:: bash

    cp /usr/share/phpPgAdmin/conf/config.inc.php-dist /usr/share/phpPgAdmin/conf/config.inc.php
    vim /usr/share/phpPgAdmin/conf/config.inc.php

Buscar ``$conf['extra_login_security']`` y poner el valor a ``false``

.. code-block:: bash

    $conf['extra_login_security'] = false;
