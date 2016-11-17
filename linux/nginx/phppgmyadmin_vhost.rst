.. _reference-linux-nginx-phppgmyadmin_vhost:

#################################
PhpPgMyAdmin Virtualhost en Nginx
#################################

Fedora
******

.. code-block:: bash

    vim /etc/nginx/conf.d/phppgadmin.local.conf

.. code-block:: bash

    server {
        listen   80;
        server_name phppgadmin.local;
        access_log /var/log/nginx/phppgadmin_access.log;
        error_log /var/log/nginx/phppgadmin_error.log;
        root /usr/share/phpPgAdmin/;

        location / {
            index  index.php;
        }

        ## Images and static content is treated different
        location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
            access_log        off;
            expires           360d;
        }

        location ~ /\.ht {
            deny  all;
        }

        location ~ /(libraries|setup/frames|setup/libs) {
            deny all;
            return 404;
        }

        location ~ \.php$ {
            include /etc/nginx/fastcgi_params;
            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME /usr/share/phpPgAdmin$fastcgi_script_name;
        }
    }

.. code-block:: bash

    systemctl restart postgresql.service
    systemctl restart nginx.service
    systemctl restart php-fpm.service

Ubuntu
******

.. code-block:: bash

    vim /etc/nginx/sites-available/phppgadmin

.. code-block:: bash

    server {
        listen   80;
        server_name phppgadmin.local;
        access_log /var/log/nginx/phppgadmin_access.log;
        error_log /var/log/nginx/phppgadmin_error.log;
        root /usr/share/phpPgAdmin/;

        location / {
            index  index.php;
        }

        ## Images and static content is treated different
        location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
            access_log        off;
            expires           360d;
        }

        location ~ /\.ht {
            deny  all;
        }

        location ~ /(libraries|setup/frames|setup/libs) {
            deny all;
            return 404;
        }

        location ~ .php$ {
            try_files $uri =404;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_index index.php;
            include /etc/nginx/fastcgi_params;
        }
    }

.. code-block:: bash

    ln -s /etc/nginx/sites-available/phppgadmin /etc/nginx/sites-enabled/phppgadmin

    service nginx restart
    service php5-fpm restart
