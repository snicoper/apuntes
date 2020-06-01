.. _reference-linux-fedora-centos-configurar_sonarqube:

####################
Configurar Sonarqube
####################

**Fuentes**

* https://www.fosslinux.com/24429/how-to-install-and-configure-sonarqube-on-centos-7.htm

Requirements
************

* Java (Oracle JRE 11 or OpenJDK 11)
* PostgreSQL 10 or 9.3–9.6

.. code-block:: bash

    su -

OpenJDK lasted
**************

Requiere JDK 11+.

Esto instala OpenJDK 14.

.. code-block:: bash

    dnf install java-latest-openjdk

Cambiar java por defecto.

.. code-block:: bash

    alternatives --config java

Postgresql
**********

* :ref:`reference-linux-postgresql-instalacion_postgresql`

.. code-block:: bash

    psql -U postgres

    CREATE USER sonar WITH PASSWORD '123456';
    CREATE DATABASE sonar WITH OWNER sonar;
    \q

Configuracion del sistema
*************************

El usuario que ejecuta Sonarqube puede abrir al menos 65536 descriptores de archivo.
El usuario que ejecuta Sonarqube puede abrir al menos 4096 hilos.

.. code-block:: bash

    vim /etc/sysctl.conf

.. code-block:: bash

    vm.max_map_count=262144
    fs.file-max=65536

Aplicar la configuración

.. code-block:: bash

    sysctl -w vm.max_map_count=262144

Sonarqube
*********

* [https://www.sonarqube.org/downloads/](https://www.sonarqube.org/downloads/)

Descomprimir Sonarqube.

.. code-block:: bash

    unzip sonarqube-8.3.1.34397.zip

.. code-block:: bash

    sudo mv sonarqube-8.3.1.34397 /opt/sonarqube

SELinux

.. code-block:: bash

    /sbin/restorecon -v /opt/sonarqube/bin/linux-x86-64/sonar.sh

    chcon -t httpd_sys_content_t /opt/sonarqube/web

Editar configuración de Sonarqube.

.. code-block:: bash

    sudo vim /opt/sonarqube/conf/sonar.properties

.. code-block:: bash

    # linea 18 y 19
    sonar.jdbc.username=sonar
    sonar.jdbc.password=123456

    # linea 36
    sonar.jdbc.url=jdbc:postgresql://localhost/sonar

    # linea 102
    sonar.web.host=0.0.0.0

    # linea 108
    sonar.web.port=9000

    # linea 406
    sonar.path.data=/var/sonarqube/data

    # Linea 407
    sonar.path.temp=/var/sonarqube/temp

Crear usuario de sistema.

.. code-block:: bash

    sudo useradd -r -s /bin/false sonar
    passwd sonar

    chown -R sonar:sonar /opt/sonarqube

.. code-block:: bash

    mkdir -p /var/sonarqube/data
    mkdir -p /var/sonarqube/temp

    chown -R sonar:sonar /var/sonarqube

Systemd service
***************

.. code-block:: bash

    vim /etc/systemd/system/sonarqube.service

.. code-block:: bash

    [Unit]
    Description=SonarQube service
    After=syslog.target network.target

    [Service]
    Type=forking
    ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
    ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
    LimitNOFILE=65536
    LimitNPROC=4096
    User=sonar
    Group=sonar
    Restart=on-failure

    [Install]
    WantedBy=multi-user.target

.. code-block:: bash

    systemctl daemon-reload
    systemctl enable sonarqube.service
    systemctl start sonarqube.service

Web Server Logs.

.. code-block:: bash

    tail -f /opt/sonarqube/logs/sonar.log

ElasticSearch logs.

.. code-block:: bash

    tail -f /opt/sonarqube/logs/es.log

Compute Engine logs.

.. code-block:: bash

    tail -f /opt/sonarqube/logs/ce.log

Nginx configure reverse proxy
*****************************

.. code-block:: bash

    dnf install -y nginx

.. code-block:: bash

    systemctl start nginx
    systemctl enable nginx

TODO: Añadir certbot.

.. code-block:: bash

    vim /etc/nginx/conf.d/sonarqube.conf

.. code-block:: bash

    server {
        listen   80;
        server_name sonar.local;

        access_log /var/log/nginx/sonar.local-access.log;
        error_log /var/log/nginx/sonar.local-error.log;

        location / {
            proxy_pass "http://127.0.0.1:9000";
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }

Editar hosts.

.. code-block:: bash

    vim /etc/hosts

.. code-block:: bash

    127.0.0.1   sonar.local

* http://sonar.local

Sonar-scanner
*************

* https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/

.. code-block:: bash

    dotnet tool install --global dotnet-sonarscanner

Script sh
*********

.. code-block:: bash

    #!/bin/bash

    # Requiere dotnet-sonarscanner.
    # dotnet tool install --global dotnet-sonarscanner

    APP_ROOT="$(dirname "$(dirname "$(readlink -fm "$0")")")"

    # WebApi
    cd $APP_ROOT/webapi

    dotnet sonarscanner begin \
    /k:"6bd9325c-d346-48b5-ab33-4993b61d1567" \
    /d:sonar.host.url="http://sonar.local" \
    /d:sonar.login="8ba567a58f7dff6a80e28e5167bb48a59e75b9dc"
    dotnet build NetClock.sln
    dotnet sonarscanner end /d:sonar.login="8ba567a58f7dff6a80e28e5167bb48a59e75b9dc"

    # WebApp
    cd $APP_ROOT/webapp

    sonar-scanner \
    -Dsonar.projectKey=NetClockApp \
    -Dsonar.sources=. \
    -Dsonar.host.url=http://sonar.local \
    -Dsonar.login=8ba567a58f7dff6a80e28e5167bb48a59e75b9dc
