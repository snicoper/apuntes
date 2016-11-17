.. _reference-linux-nginx-phpmyadmin_vhost:

.. |br| raw:: html

   <br />

################################
PhpMyAdmin Virtualhost en Nginx
################################

Tener instalado MySQL o MariaDB + PHP.

Fedora
******

.. code-block:: bash

    sudo vim /etc/nginx/conf.d/phpmyadmin.local.conf

.. code-block:: bash

    server {
        listen   80;
        server_name phpmyadmin.local;
        access_log /var/log/nginx/phpmyadmin_access.log;
        error_log /var/log/nginx/phpmyadmin_error.log;
        root /usr/share/phpMyAdmin;

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
            fastcgi_param SCRIPT_FILENAME /usr/share/phpMyAdmin$fastcgi_script_name;
        }
    }

.. code-block:: bash

    systemctl restart nginx.service
    systemctl restart php-fpm.service

Ubuntu
******

.. code-block:: bash

    vim /etc/nginx/sites-available/phpmyadmin

.. code-block:: bash

    server {
        listen   80;
        server_name phpmyadmin.local;
        access_log /var/log/nginx/phpmyadmin_access.log;
        error_log /var/log/nginx/phpmyadmin_error.log;
        root /usr/share/phpMyAdmin;

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

    ln -s /etc/nginx/sites-available/phpmyadmin /etc/nginx/sites-enabled/phpmyadmin

    sudo service nginx restart
    sudo service php5-fpm restart

