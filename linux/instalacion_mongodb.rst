.. _reference-linux-instalacion_mongodb:

####################
Instalación MongoDb
####################

Fedora
******

.. code-block:: bash

    dnf install mongodb mongodb-server

    systemctl enable mongod.service
    systemctl start mongod.service

Ubuntu
******

.. code-block:: bash

    sudo apt-get install mongodb mongodb-server
