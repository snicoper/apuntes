.. _reference-linux-ubuntu-crear_certificado_ssl:

#####################
Crear certificado SSL
#####################

Pongo el nombre de ofervivienda para el servidor principal, cambiar si es otro servidor

.. code-block:: bash

    sudo -s

    cd /etc/ssl/private

.. code-block:: bash

    openssl genrsa -des3 -out ofervivienda.key 2048

.. code-block:: bash

    openssl req -new -days 3650 -key ofervivienda.key -out ofervivienda.csr

.. code-block:: console

    Country Name (2 letter code) [XX]:es
    State or Province Name (full name) []:Spain
    Locality Name (eg, city) [Default City]:Barcelona
    Organization Name (eg, company) [Default Company Ltd]:snicoper
    Organizational Unit Name (eg, section) []:nombre_org
    Common Name (eg, your name or your server's hostname) []:ofervivienda.workspace.local
    Email Address []:snicoper@gmail.com

    A challenge password []: (Intro)
    An optional company name []: (Intro)

.. code-block:: bash

    openssl x509 -in ofervivienda.csr -out ofervivienda.crt -req -signkey ofervivienda.key -days 3650

.. code-block:: bash

    chmod 400 ofervivienda.*
