.. _reference-linux-nginx-authentication_nginx:

#########################
Authentication HTTP Nginx
#########################

**Fuentes**

* https://www.digitalocean.com/community/tutorials/how-to-set-up-basic-http-authentication-with-nginx-on-centos-7

----

.. code-block:: bash

    su -
    yum install -y httpd-tools

    cd /etc/nginx/

    # Donde el nginx es el nombre que después pedirá
    # y .htpasswd el archivo que generara.
    htpasswd -c /etc/nginx/.htpasswd nginx

Editar en el servidor:

.. code-block:: bash

    vim /etc/nginx/conf.d/archivo_configuracion.conf

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        auth_basic "Private Property";
        auth_basic_user_file /etc/nginx/.htpasswd;

        # ....

.. code-block:: bash

    systemctl reload nginx
