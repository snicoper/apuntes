.. _reference-linux-fedora-centos-certificado_lets_encrypt:

#########################
Certificado Let's Encrypt
#########################

**Fuentes**

https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-centos-7

----------

Probado en **Fedora** y **Centos**

.. code-block:: bash

    yum install certbot

.. code-block:: bash

    vim /etc/nginx/default.d/le-well-known.conf

.. code-block:: bash

    location ~ /.well-known {
      allow all;
    }

    systemctl restart nginx

.. code-block:: bash

    certbot certonly -a webroot --webroot-path=/usr/share/nginx/html -d MIDOMINIO.com -d www.MIDOMINIO.com -d mail.MIDOMINIO.com

Pide un email, cuando todo haya salido bien.

.. code-block:: bash

    openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048

Actualizar el certificado, dura 3 meses.

.. code-block:: bash

    certbot renew

Cron
****

.. code-block:: bash

    sudo crontab -e

.. code-block:: bash

    MAILTO=MIUSUARIO@MIDOMINIO.com

    30 2 * * 1 /usr/bin/certbot renew >> /var/log/le-renew.log
    35 2 * * 1 /usr/bin/systemctl reload nginx

Nginx
*****

Para **Nginx** uso esta plantilla: https://github.com/snicoper/django-boilerplate/blob/master/compose/configs/nginx_https.conf

Quitar de ``/etc/nginx/nginx.conf`` ``default_server`` o dará error.

Postfix
*******

Para la configuración de :ref:`reference-linux-fedora-centos-postfix`

En ``vim /etc/postfix/main.cf``

.. code-block:: bash

    smtpd_tls_cert_file = /etc/letsencrypt/live/MIDOMINIO.com/fullchain.pem
    smtpd_tls_key_file = /etc/letsencrypt/live/MIDOMINIO.com/privkey.pem

Y en ``/etc/dovecot/conf.d/10-ssl.conf``

.. code-block:: bash

    ssl_cert = </etc/letsencrypt/live/MIDOMINIO.com/fullchain.pem
    ssl_key = </etc/letsencrypt/live/MIDOMINIO.com/privkey.pem

Firewalld
*********

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --add-service=https
    firewall-cmd --reload
