.. _reference-linux-fedora-centos-crear_ssl:

#########
Crear SSL
#########
.. code-block:: bash

    cd /etc/pki/tls/certs
    make snicoper.key

Introducir passphrase

.. code-block:: bash

    umask 77 ; \
    /usr/bin/openssl genrsa -aes128 2048 > snicoper.key

    openssl rsa -in snicoper.key -out snicoper.key

    make snicoper.csr

Los datos que le pongo (Son para servidor de pruebas!)

.. code-block:: console

    Country Name (2 letter code) [XX]:es
    State or Province Name (full name) []:Spain
    Locality Name (eg, city) [Default City]:Barcelona
    Organization Name (eg, company) [Default Company Ltd]:snicoper
    Organizational Unit Name (eg, section) []:Web service
    Common Name (eg, your name or your server's hostname) []:ns1
    Email Address []:snicoper@gmail.com

    Please enter the following 'extra' attributes
    to be sent with your certificate request
    A challenge password []:(vacio)
    An optional company name []: (vacio)

.. code-block:: bash

    openssl x509 -in snicoper.csr -out snicoper.crt -req -signkey snicoper.key -days 3650

    chmod 400 snicoper.*
