.. _reference-linux-fedora-centos-crear_ssl:

#########
Crear SSL
#########

* https://linode.com/docs/security/ssl/create-a-self-signed-tls-certificate/

.. code-block:: bash

    cd /etc/pki/tls/certs
    openssl req -new -newkey rsa:4096 -x509 -sha256 -days 365 -nodes -out snicoper.crt -keyout snicoper.key

.. code-block:: bash

    chmod 400 snicoper.*
