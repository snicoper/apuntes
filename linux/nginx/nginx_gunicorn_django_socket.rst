.. _reference-linux-nginx-nginx_gunicorn_django_socket:

############################
Nginx Gunicorn Django Socket
############################

Servir un sitio Web Django con gunicorn y Nginx es algo que tarde o temprano todos hacemos, aunque
solo sea para ver como responde nuestro sitio antes de ponerlo en producción y lidiar con los
problemas que nos podemos encontrar cuando de verdad lo subamos a un servidor.

Esta es una configuración básica que funciona muy bien.

En primer lugar, instalamos nginx

.. code-block:: bash

    sudo dnf install nginx

Primero creamos un entorno virtual con ``virtualenvwrapper``.

.. code-block:: bash

    mkvirtualenv practica

El resto del ejemplo, estaremos usando el entorno virtual ``practica``.

Instalar Django y Gunicorn con ``pip``.

.. code-block:: bash

    pip install django
    pip install gunicorn

Creamos un directorio para todo el proyecto en ``~/webapps/`` yo para los ejemplos, uso mi usuario
``snicoper``, tu siempre pon tu usuario!.

.. code-block:: bash

    cd ~/webapps
    mkdir example.com


Creamos unos directorios dentro de ``example.com``

.. code-block:: bash

    cd example.com
    mkdir bin run

Y ahora, creamos el proyecto Django, también dentro de ``example.com``

.. code-block:: bash

    django-admin startproject example

Esto nos crea el típico proyecto Django

.. code-block:: console

    .
    ├── bin
    ├── example
    │   ├── example
    │   │   ├── __init__.py
    │   │   ├── settings.py
    │   │   ├── urls.py
    │   │   └── wsgi.py
    │   └── manage.py
    └── run

Crearemos un archivo ``gunicorn_start.sh`` en el directorio ``bin/``.

.. code-block:: bash

    vim bin/gunicorn_start.sh

y añadimos las siguientes lineas

.. code-block:: bash

    #!/bin/bash

    NAME="example.com" # Name of the application
    DJANGODIR=/home/snicoper/webapps/example.com/example # Django project directory
    LOGFILE=/var/log/gunicorn/gunicorn.log
    LOGDIR=$(dirname $LOGFILE)
    SOCKFILE=/home/snicoper/webapps/example.com/run/gunicorn.sock # we will communicate using this unix socket
    USER=snicoper # the user to run as
    GROUP=snicoper # the group to run as
    NUM_WORKERS=3 # how many worker processes should Gunicorn spawn
    DJANGO_SETTINGS_MODULE=example.settings # which settings file should Django use
    DJANGO_WSGI_MODULE=example.wsgi # WSGI module name

    echo "Starting $NAME as `whoami`"

    # Activate the virtual environment
    source /home/snicoper/.virtualenvs/example.com/bin/activate
    export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
    export PYTHONPATH=$DJANGODIR:$PYTHONPATH

    # Create the run directory if it doesn't exist
    RUNDIR=$(dirname $SOCKFILE)
    test -d $RUNDIR || mkdir -p $RUNDIR

    # Start your Django Unicorn
    # Programs meant to be run under supervisor should not daemonize themselves (do not use --daemon)
    exec gunicorn ${DJANGO_WSGI_MODULE}:application \
    --name $NAME \
    --workers $NUM_WORKERS \
    --user=$USER --group=$GROUP \
    --bind=unix:$SOCKFILE \
    --log-level=debug \
    --log-file=$LOGFILE 2>>$LOGFILE

Actualizar las rutas y usuario/grupo del script, y le damos permisos de ejecución.

.. code-block:: bash

    chmod +x bin/gunicorn_start.sh

Crear directorio ``/var/log/gunicorn`` y dentro, el archivo ``gunicorn.log``

.. code-block:: bash

    sudo mkdir /var/log/gunicorn
    sudo chown snicoper:snicoper /var/log/gunicorn
    touch /var/log/gunicorn/gunicorn.log

Y por ultimo, configurar un servidor virtual de nginx, para ello, creamos un archivo en
``etc/nginx/conf.d/example.com.conf``

.. code-block:: bash

    sudo vim etc/nginx/conf.d/example.com.cof

Y añadimos lo siguiente, una vez mas, asegurase que las rutas son las correctas y el usuario.

.. code-block:: nginx

    upstream example_app_server {
      # fail_timeout=0 means we always retry an upstream even if it failed
      # to return a good HTTP response (in case the Unicorn master nukes a
      # single worker for timing out).

      server unix:/home/snicoper/webapps/example.com/run/gunicorn.sock fail_timeout=0;
    }

    server {

        listen   80;
        server_name example.com;

        client_max_body_size 4G;

        access_log /var/log/nginx/example.com-access.log;
        error_log /var/log/nginx/example.com-error.log;

        location /static/ {
            alias   /home/snicoper/webapps/example.com/static/;
        }

        location /media/ {
            alias   /home/snicoper/webapps/example.com/media/;
        }

        location / {
            # an HTTP header important enough to have its own Wikipedia entry:
            #   http://en.wikipedia.org/wiki/X-Forwarded-For
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

            # enable this if and only if you use HTTPS, this helps Rack
            # set the proper protocol for doing redirects:
            # proxy_set_header X-Forwarded-Proto https;

            # pass the Host: header from the client right along so redirects
            # can be set properly within the Rack application
            proxy_set_header Host $http_host;

            # we don't want nginx trying to do something clever with
            # redirects, we set the Host: header above already.
            proxy_redirect off;

            # set "proxy_buffering off" *only* for Rainbows! when doing
            # Comet/long-poll stuff.  It's also safe to set if you're
            # using only serving fast clients with Unicorn + nginx.
            # Otherwise you _want_ nginx to buffer responses to slow
            # clients, really.
            # proxy_buffering off;

            # Try to serve static files from nginx, no point in making an
            # *application* server like Unicorn/Rainbows! serve static files.
            if (!-f $request_filename) {
                proxy_pass http://example_app_server;
                break;
            }
        }

        # Error pages
        error_page 500 502 503 504 /500.html;
        location = /500.html {
            root /home/snicoper/webapps/example.com/templates/;
        }
    }

Reiniciamos el servidor nginx con

.. code-block:: bash

    sudo systemctl start nginx.service

    # Si lo queremos como servicio.
    sudo systemctl enable nginx.service

Abrir el puesto 80

.. code-block:: bash

    sudo firewall-cmd --permanent --zone=public --add-service=http
    sudo firewall-cmd --reload

Para la practica, el puerto no es necesario, pero hay queda :), y ahora le en ``/etc/hosts`` le
decimos que ``example.com`` apunte a ``127.0.0.1``

.. code-block:: bash

    sudo vim /etc/hosts

    # Añadimos
    127.0.0.1   example.com

Primero lo probamos manualmente

.. code-block:: bash

    cd ~/webapps/example.com/bin
    ./gunicorn_start.sh

Entramos a [http://example.com](http://example.com)

Lo mas seguro que SELinux se queje con algo así **SELinux is preventing nginx from write access on the sock_file gunicorn.sock.**.

Yo, para solucionar eso hice lo siguiente:

.. code-block:: bash

    cd ~/webapps/example.com/run/

    sudo grep nginx /var/log/audit/audit.log | audit2allow -M nginx
    sudo semodule -i nginx.pp

Ya con eso, me funciono bien. Ahora, ya solo nos falta poner que ``gunicorn_start.sh`` se inicie al
reiniciar la maquina y poderlo reiniciar de una manera rápida.

Casi todo el mundo lo hace con ``supervisor``, pero yo probé creando un servicio systemd y me funciona
muy bien, así que es como lo voy a poner.

.. code-block:: bash

    sudo vim /etc/systemd/system/gunicorn.service

Y añadimos los siguiente

.. code-block:: bash

    [Unit]
    Description=gunicorn daemon
    After=syslog.target
    After=network.target

    [Service]
    PIDFile=/run/gunicorn/pid
    User=snicoper
    Group=snicoper
    WorkingDirectory=/home/snicoper/webapps/example.com/bin/
    ExecStart=/bin/bash gunicorn_start.sh
    ExecReload=/bin/kill -s HUP $MAINPID
    ExecStop=/bin/kill -s TERM $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target

Para reiniciar, etc, se usa los típicos comandos de systemd

.. code-block:: bash

    sudo systemctl start gunicorn.service
    sudo systemctl stop gunicorn.service
    sudo systemctl restart gunicorn.service
    sudo systemctl enable gunicorn.service

Esta configuración ha sido por socket entre gunicorn y nginx, pero también es posible hacerlo por IP,
tengo unos [apuntes sobre el tema](http://apuntes-snicoper.readthedocs.org/es/latest/linux/nginx/nginx_gunicorn_django.html).

---

**Fuentes**

* [http://gunicorn-docs.readthedocs.org/en/latest/index.html](http://gunicorn-docs.readthedocs.org/en/latest/index.html)
* [https://gist.github.com/postrational/5747293](https://gist.github.com/postrational/5747293)
* [http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/](http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/)
* [http://superuser.com/questions/809527/nginx-cant-connect-to-uwsgi-socket-with-correct-permissions](http://superuser.com/questions/809527/nginx-cant-connect-to-uwsgi-socket-with-correct-permissions)
