.. _reference-linux-nginx-nginx_gunicorn_django:

####################################
Instalación Nginx, Gunicorn y Django
####################################

**Fuentes**

* http://goodcode.io/blog/django-nginx-gunicorn/
* http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/
* https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-django-with-postgres-nginx-and-gunicorn

----------

Gunicorn
********

En ``proyect_name/bin``, creamos un archivo ``gunicorn_start.sh``

.. code-block:: bash

    vim bin/gunicorn_start.sh

    # Añadimos

    #!/bin/bash

    NAME="proyect_name" # Name of the application
    DJANGODIR=/home/snicoper/projects/python/proyect_name/src/ # Django project directory
    LOGFILE=/home/snicoper/projects/python/proyect_name/logs/gunicorn.log
    LOGDIR=$(dirname $LOGFILE)
    USER=snicoper # the user to run as
    GROUP=snicoper # the group to run as
    ADDRESS=127.0.0.1:8001
    NUM_WORKERS=3 # how many worker processes should Gunicorn spawn
    DJANGO_SETTINGS_MODULE=settings.settings_prod # which settings file should Django use
    DJANGO_WSGI_MODULE=settings.wsgi # WSGI module name

    echo "Starting $NAME as `whoami`"

    # Activate the virtual environment
    cd $DJANGODIR
    source /home/snicoper/.virtualenvs/default/bin/activate
    export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
    export PYTHONPATH=$DJANGODIR:$PYTHONPATH

    # Start your Django Unicorn
    # Programs meant to be run under supervisor should not daemonize themselves (do not use --daemon)
    exec gunicorn ${DJANGO_WSGI_MODULE}:application \
        --workers $NUM_WORKERS \
        --bind=$ADDRESS \
        --user=$USER --group=$GROUP \
        --log-level=debug \
        --log-file=$LOGFILE 2>>$LOGFILE

.. warning::
    Corregir las rutas y usuario!

Permisos de ejecución

.. code-block:: bash

    chmod +x bin/gunicorn_start.sh


Nginx
*****

:ref:`reference-linux-nginx-instalacion_nginx`

.. note::
    En Fedora/Centos si se sirven las paginas en el ``home`` hay que dar permisos
    al home del usuario ``chmod 711 /home/usuario``

.. code-block:: bash

    # Ubuntu
    sudo vim /etc/nginx/sites-avalaible/proyect_name

    # Fedora/Centos
    sudo vim /etc/nginx/conf.d/proyect_name.conf

Añadimos

.. code-block:: bash

    server {
        listen   80;
        server_name www.workspace.local;

        access_log /var/log/nginx/proyect_name-access.log;
        error_log /var/log/nginx/proyect_name-error.log;

        # Django media
        location /media/  {
            alias /home/snicoper/projects/python/proyect_name/src/media/;  # your Django project's media files - amend as required
        }

        # Django static
        location /static/ {
            alias /home/snicoper/projects/python/proyect_name/src/static/; # your Django project's static files - amend as required
        }

        # Django static admin
        location /static/admin/ {
            # this changes depending on your python version
            alias /home/snicoper/.virtualenvs/default/lib/python3.4/site-packages/django/contrib/admin/static/admin/;
        }

        location / {
            proxy_pass_header Server;
            proxy_set_header Host $http_host;
            proxy_redirect off;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Scheme $scheme;
            proxy_connect_timeout 10;
            proxy_read_timeout 10;
            proxy_pass http://localhost:8001/;
        }

        # what to serve if upstream is not available or crashes
        error_page 500 502 503 504 /templates/50x.html;
    }

.. code-block:: bash

    # Solo Ubuntu
    sudo ln -s /etc/nginx/sites-avalaible/proyect_name /etc/nginx/sites-enabled/proyect_name

Si los archivos static no se ven, mirar ``collectstatic`` de Django, o modificar
``location /static/admin/``

En Fedora/Centos, mirar :ref:`reference-linux-fedora-centos-reglas_selinux` y si el
proyecto esta en el ``home`` de un usuario, poner permisos ``711`` en el directorio
del usuario, de lo contrario, mostrara un error ``403``

Reiniciar nginx

.. code-block:: bash

    # Ubuntu
    sudo service nginx restart

    # Fedora/Centos
    systemctl restart nginx.service

Supervisor
**********

**Ubuntu**

.. code-block:: bash

    sudo apt-get install supervisor
    sudo touch /etc/supervisor/conf.d/proyect_name.conf

Añadir en ``proyect_name.conf``

.. code-block:: bash

    [program:proyect_name]
    command=/home/snicoper/projects/python/proyect_name/bin/gunicorn_start.sh
    user=snicoper
    stdout_logfile=/home/snicoper/projects/python/proyect_name/logs/gunicorn_supervisor.log
    redirect_stderr=true
    autostart=true
    autorestart=true

Crear archivo de log

.. code-block:: bash

    mkdir /home/snicoper/projects/python/proyect_name/logs
    touch /home/snicoper/projects/python/proyect_name/logs/gunicorn_supervisor.log

.. code-block:: bash

    sudo supervisorctl reread
    sudo supervisorctl update

**Comandos supervisor**

.. code-block:: bash

    sudo supervisorctl status proyect_name
    sudo supervisorctl stop proyect_name
    sudo supervisorctl start proyect_name
    sudo supervisorctl restart proyect_name

Systemd
*******

**Fedora/Centos7 como servicio**

.. code-block:: bash

    sudo vim /etc/systemd/system/gunicorn.service

    [Unit]
    Description=gunicorn daemon
    After=syslog.target
    After=network.target

    [Service]
    PIDFile=/run/gunicorn/pid
    User=snicoper
    Group=snicoper
    WorkingDirectory=/home/snicoper/www/sitio/bin/
    ExecStart=/bin/bash gunicorn_start.sh
    ExecReload=/bin/kill -s HUP $MAINPID
    ExecStop=/bin/kill -s TERM $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target

.. code-block:: bash

    sudo systemctl start gunicorn.service
    sudo systemctl stop gunicorn.service
    sudo systemctl restart gunicorn.service
    sudo systemctl enable gunicorn.service
