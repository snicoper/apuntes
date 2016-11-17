.. _reference--windows-instalacion_nginx_php_windows:

#######################
Nginx y PHP en Windows
#######################

* Descargar `php <http://windows.php.net/download>`_ ``Non Thread Safe``
* Descargar `nginx <http://nginx.org/>`_
* Descargar `NSSM (Non-Sucking Service Manager) <https://nssm.cc/>`_

Descomprimir los 3 archivos y re nombrarlos son la versión (opcional), mover a ``C:\`` (opcional), quedando de la siguiente manera:

.. code-block:: bash

    C:\nginx
    C:\php
    C:\nssm

Añadir al ``path``

.. code-block:: bash

    C:\nginx;C:\php;C:\nssm\win64;

Configuración de Nginx
**********************

Editar ``C:\nginx\conf\nginx.conf``

.. code-block:: bash

    http {
        # ...

        # Añadir al final de http { la siguiente linea

        include C:/nginx/conf/vhosts/*.conf;
    }

Crear directorio ``C:/nginx/conf/vhosts``, es donde estaran los host virtuales de nginx.
Crear en el directorio de usuario ``~/Projects/www``

Crear ``C:/nginx/conf/vhosts/snicoper.dev.conf`` y añadir:

.. code-block:: bash

    server {
        listen 80;
        server_name snicoper.dev;
        access_log logs/snicoper.dev-access.log;
        error_log logs/snicoper.dev-error.log;
        root C:/Users/snicoper/Projects/www;

        location / {
            index index.html index.htm index.php;
        }

        location ~* \.(jpg|jpeg|gif|png|css|js|ico|xml)$ {
            access_log        off;
            log_not_found     off;
            expires           360d;
        }

        # Si quiero que se vean los archivos y directorios cambiar a on
        autoindex on;

        location ~ \.php$ {
            fastcgi_pass  127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME C:/Users/snicoper/Projects/www$fastcgi_script_name;
        }
    }

Configuración de php
********************

Entrar en ``C:\php`` copiar/pegar ``php.ini-development`` y renombrarlo a ``php.ini``

Editar ``C:\php\php.ini``

.. code-block:: ini

    ; Linea 736, descomentar
    extension_dir = "ext"

    ; Linea 927, descomentar y añadir zona horaria
    date.timezone = Europe/Madrid

    ; A partir de la linea 878, descomentar las extensiones necesarias

Configuración de Nssm
*********************

Entrar en una terminal (Símbolo del sistema) como administrador:

.. code-block:: bash

    nssm install nginxd

    # Path:
    C:\nginx\nginx.exe

    # Startup directory:
    C:\nginx

    # Pulsar 'Edit service'

    nssm install phpcgid

    # Path:
    C:\php\php-cgi.exe

    # Startup directory:
    C:\php

    # Arguments:
    -b 127.0.0.1:9000

    # Pulsar 'Edit service'

Iniciar servicios

.. code-block:: bash

    nssm start nginxd
    nssm start phpcgid

Para ver el resto de comandos escribir solo ``nssm``, al iniciar se los servicios se iniciaran solos.

Para probar crear archivo ``~/Projects/www/test.php`` añadiendo ``<?php phpinfo();``

.. note::

    Es necesario añadir al archivo ``host`` ``127.0.0.1 snicoper.dev``

XDebug
******

Abrimos la terminal y ejecutamos:

.. code-block:: bash

    php -i > phpini.txt

Abrimos el archivo ``phpini.txt`` y copiamos su contenido. Ahora vamos a `Xdebug <http://xdebug.org/wizard.php>`_ ,lo pegamos en el textarea y le damos al boton ``Analyse my phpinfo() output``.

Nos mostrara que descarga tenemos que hacer.

Descargar el archivo y renombrar a ``php_xdebug.dll``, después, copiar el archivo en ``C:\php\ext``, por ultimo editar el archivo ``C:\php\php.ini`` y añadir al final:

.. code-block:: bash

    zend_extension = C:\php\ext\php_xdebug.dll

Composer
********

`Descargar composer <https://getcomposer.org/download/>`_ y seguir las instrucciones del instalador, la única nota es que en el ``php.ini`` se ha de descomentar la linea ``extension=php_openssl.dll`` antes de comenzar la instalación.
