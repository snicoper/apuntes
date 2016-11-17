.. _reference-linux-apache-apache_virtualhost:

##################
Apache Virtualhost
##################

Siempre creo los entornos en el ``~/usuario/public_html``
pero se podría poner donde uno quiera.

Fedora
******

Como root todo

.. code-block:: bash

    mkdir /home/snicoper/public_html
    chmod 711 /home/snicoper
    chmod 755 /home/snicoper/public_html
    chown snicoper:snicoper /home/snicoper/public_html

Ubuntu
******

.. code-block:: bash

    mkdir /home/snicoper/public_html

Crear virtualhost, fedora y ubuntu
**********************************

.. code-block:: bash

    # Fedora
    vim /etc/httpd/conf.d/workspace.local.conf

    # Ubuntu
    sudo vim /etc/apache2/sites-available/workspace.local

.. code-block:: bash

    <VirtualHost *:80>
        DocumentRoot /home/snicoper/public_html
        ServerName www.workspace.local
        ServerAlias www.workspace.local
        DirectoryIndex index.php
        ServerAdmin snicoper@gmail.com
        ErrorLog /var/log/httpd/workspace.local-error_log
        CustomLog /var/log/httpd/workspace.local-access_log combined
        <Directory /home/snicoper/public_html>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
            Require all granted
        </Directory>
    </VirtualHost>

Ubuntu
******

.. code-block:: bash

    a2enmod rewrite
    a2dissite default
    a2ensite workspace.local

SELinux
=======

Ver :ref:`reference-linux-fedora-centos-reglas_selinux`

SSL
***

Fedora
=======

.. code-block:: bash

    yum install mod_ssl
    mkdir /etc/httpd/ssl
    openssl req -new -x509 -days 365 -nodes -out /etc/httpd/ssl/httpd.pem -keyout /etc/httpd/ssl/httpd.key

.. code-block:: console

    Country Name (2 letter code) [XX]:es
    State or Province Name (full name) []:Spain
    Locality Name (eg, city) [Default City]:Barcelona
    Organization Name (eg, company) [Default Company Ltd]:snicoper
    Organizational Unit Name (eg, section) []:personal
    Common Name (eg, your name or your server's hostname) []:lxmaq1.workspace.local
    Email Address []:snicoper@gmail.com

Ahora es cada virtual host, hacer una copia y modificar

.. code-block:: bash

    cp /etc/httpd/conf.d/workspace.conf /etc/httpd/conf.d/ssl.workspace.conf

.. code-block:: bash

    vim /etc/httpd/conf.d/ssl.workspace.conf

.. code-block:: bash

    <VirtualHost *:443>
        SSLEngine On
        SSLCertificateFile /etc/httpd/ssl/httpd.pem
        SSLCertificateKeyFile /etc/httpd/ssl/httpd.key

        DocumentRoot /home/snicoper/public_html
        ServerName www.workspace.local
        ServerAdmin snicoper@gmail.com
        ErrorLog /var/log/httpd/workspace.local-error_log
        CustomLog /var/log/httpd/workspace.local-access_log combined
        <Directory /home/snicoper/public_html>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
            Require all granted
        </Directory>
    </VirtualHost>

Ubuntu
======

**POR HACER**
