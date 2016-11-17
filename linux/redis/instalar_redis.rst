.. _reference-linux-redis-instalar_redis:

##############
Instalar Redis
##############

**Fuentes**

* http://redis.io/

-----

Fedora
======

.. code-block:: bash

    dnf install -y redis
    systemctl start redis.service
    systemctl enable redis.service
    
Ubuntu
======

.. code-block:: bash

    sudo apt-get install redis-server

Backup del archivo de configuración

.. code-block:: bash

    cp /etc/redis/redis.conf /etc/redis/redis.conf.default
