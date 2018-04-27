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

En mi caso lo instalo en una maquina virtual y solo abro puertos para lan

.. code-block:: bash

    firewall-cmd --permanent --zone=trusted --add-source=192.168.122.0/24
    firewall-cmd --reload

Si no, abrir puerto ``1433``

.. code-block:: bash

    firewall-cmd --zone=public --add-port=1433/tcp --permanent
    firewall-cmd --reload

.. code-block:: bash

    # Como usuario
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
    source ~/.bashrc

Por ultimo me creo un usuario `snicoper` con un password fácil,

.. code-block:: bash

    CREATE LOGIN snicoper WITH PASSWORD = '123456', CHECK_POLICY = OFF;
    EXEC sp_addsrvrolemember 'snicoper', 'sysadmin';
