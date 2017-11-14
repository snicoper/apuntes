.. _reference-linux-fedora-centos-bind_fedora:

####
Bind
####

.. code-block:: bash

    dnf install -y bind bind-utils

.. code-block:: bash

    echo 'OPTIONS="-4"' >> /etc/sysconfig/named

.. code-block:: bash

    vim /etc/named.conf

.. code-block:: bash

    # Linea 11
    listen-on port 53 { 127.0.0.1; 192.168.1.0/24; };

    # Linea 17
    allow-query     { localhost; 192.168.1.0/24; };

Añadir después de ``logging { #.... }``

.. code-block:: bash

    zone "snicoper.local" {
        type master;
        file "snicoper.local";
        allow-update { none; };
    };

    zone "1.168.192.in-addr.arpa" IN {
        type master;
        file "reverse.snicoper.local";
        allow-update { none; };
    };

.. code-block:: bash

    vim /var/named/snicoper.local

.. code-block:: bash

    $TTL 86400
    @       IN      SOA     snicoper.local. hostmaster.snicoper.local. (
                                   2013042201      ; Serial
                                   43200      ; Refresh
                                   3600       ; Retry
                                   3600000    ; Expire
                                   2592000 )  ; Minimum

    ;       Define the nameservers and the mail servers

                    IN      NS      ns1.snicoper.local.

                    IN      A       192.168.1.100

                    IN      MX      10 mail.snicoper.local.

    mail            IN      A       192.168.1.100
    ns1             IN      A       192.168.1.100
    www             IN      CNAME   ns1

.. code-block:: bash

    vim /var/named/reverse.snicoper.local

.. code-block:: bash

    $TTL 86400
    @       IN      SOA     snicoper.local. hostmaster.snicoper.local. (
                                   2013042201      ; Serial
                                   43200      ; Refresh
                                   3600       ; Retry
                                   3600000    ; Expire
                                   2592000 )  ; Minimum

                IN      NS      ns1.snicoper.local.

    100         IN      PTR     ns1.snicoper.local.

En ``/etc/sysconfig/network-scripts/ifcfg-*`` al menos tener lo siguiente:

.. code-block:: bash

    BOOTPROTO=none
    PEERDNS=no
    DOMAIN="snicoper.local"
    IPADDR=192.168.1.100
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1
    DNS1=127.0.0.1
    DNS2=8.8.8.8
    DNS3=8.8.4.4

.. code-block:: bash

    systemctl restart NetworkManager.service

SELinux y firewall
==================

:ref:`reference-linux-fedora-centos-reglas_selinux`

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=dns
    firewall-cmd --reload
    systemctl start named.service
    systemctl enable named.service
