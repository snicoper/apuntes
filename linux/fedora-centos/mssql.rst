.. _reference-linux-fedora-centos-mssql:

##############################
Instalar MSSQL Server Centos 7
##############################

.. code-block:: bash

    su -

    curl https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo -o /etc/yum.repos.d/mssql-server-2017.repo
    curl https://packages.microsoft.com/config/rhel/7/prod.repo -o /etc/yum.repos.d/msprod.repo

    yum install mssql-server mssql-tools unixODBC-devel

.. code-block:: bash

    /opt/mssql/bin/mssql-conf setup

.. code-block:: bash

    systemctl start mssql-server
    systemctl enabled mssql-server

.. code-block:: bash

    firewall-cmd --zone=public --add-port=1433/tcp --permanent
    firewall-cmd --reload

.. code-block:: bash

    # Como usuario
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
    source ~/.bashrc
