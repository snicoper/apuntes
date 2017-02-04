.. _reference-linux-ubuntu-bind:

####
Bind
####

Fuentes
*******

* http://www.belinuxmyfriend.com/2007/07/ip-estatica-en-ubuntu-manualmente.html
* http://www.server-world.info/en/note?os=Ubuntu_13.04&p=dns&f=1
* http://lani78.com/2012/07/22/setting-up-a-dns-for-the-local-network-on-the-ubuntu-12-04-precise-pangolin-server/
* http://docs.fedoraproject.org/en-US/Fedora/20/html/Networking_Guide/index.html

Instalación
***********

.. code-block:: bash

    sudo apt install bind9 bind9utils

Configuración Red
*****************

.. code-block:: bash

    sudo vim /etc/network/interfaces

.. code-block:: bash

    auto eth0
    iface eth0 inet static
        address 192.168.1.10
        netmask 255.255.255.0
        gateway 192.168.1.1
        network 192.168.1.0
        dns-nameservers 192.168.1.10 8.8.4.4 8.8.8.8
        dns-search ns1.workspace.local
        dns-domain workspace.local

Configuración Bind
******************

.. code-block:: bash

    sudo vim /etc/bind/named.conf.options

    # En forwarders
    forwarders {
        89.36.215.212;
        8.8.8.8;
        8.8.4.4;
    };

    auth-nxdomain no;    # conform to RFC1035
    #listen-on-v6 { any; };
    listen-on port 53 { 127.0.0.1; 89.36.215.212; };
    allow-query     { any; };
    allow-transfer { any; };


.. code-block:: bash

    sudo vim /etc/bind/named.conf.local

.. code-block:: bash

    zone "ofervivienda.com" IN {
        type master;
        file "/etc/bind/db.ofervivienda";
    };

    zone "36.215.89.in-addr.arpa" IN {
        type master;
        file "/etc/bind/db.89.36.215.212";
    };

.. code-block:: bash

    sudo vim /etc/bind/db.ofervivienda

.. code-block:: bash

    $TTL 86400
    @       IN      SOA     ofervivienda.com. hostmaster.ofervivienda.com. (
                                   2013042201      ; Serial
                                   43200      ; Refresh
                                   3600       ; Retry
                                   3600000    ; Expire
                                   2592000 )  ; Minimum

    ;       Define the nameservers and the mail servers

                    IN      NS      ns1.ofervivienda.com.

                    IN      A       89.36.215.212

                    IN      MX      10 mail.ofervivienda.com.

    mail            IN      A       89.36.215.212
    ns1             IN      A       89.36.215.212
    www             IN      CNAME   ofervivienda.com.

.. code-block:: bash

    sudo vim /etc/bind/db.89.36.215.212

.. code-block:: bash

    $TTL 86400
    @       IN      SOA     ofervivienda.com. hostmaster.ofervivienda.com. (
                                   2013042201      ; Serial
                                   43200      ; Refresh
                                   3600       ; Retry
                                   3600000    ; Expire
                                   2592000 )  ; Minimum

    @           IN      NS      ns1.ofervivienda.com.

                IN      PTR     ofervivienda.com.

    212         IN      PTR     ns1.ofervivienda.com.

.. code-block:: bash

    systemctl start bind9
    systemctl enable bind9

    ufw allow 53
