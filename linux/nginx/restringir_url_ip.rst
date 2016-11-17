.. _reference-linux-nginx-restringir_url_ip:

########################
Restringir una URL a IPs
########################

**Fuentes**

* https://www.nginx.com/resources/admin-guide/restricting-access/

------

Restringir acceso a una URL a cierta/s IPs

.. code-block:: nginx

    server {
        # ....

        # Bloquear todas las ips a la administración
        # excepto a ips de la red local
        location ^~ /admin/ {
            proxy_pass http://127.0.0.1:8001;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;

            allow ip_1 o 192.168.1.0/24;
            allow ip_2;
            deny all;
        }

        # ....
    }
