.. _reference-linux-fedora-centos-configurar_red:

##############
Configurar Red
##############

**Fuentes**

* http://superuser.com/questions/645487/static-ip-address-with-networkmanager

----

Como administrador e ir a donde están los archivos de red.

.. code-block:: bash

    su
    cd /etc/sysconfig/network-scripts/

Editar según la interface que use.

.. code-block:: bash

    vim ifcfg-p2p1

.. note::
    Cuidado no tocar algunas variables como **UUID o HWADDR**.

.. code-block:: bash

    TYPE=Ethernet
    BOOTPROTO=none
    DEFROUTE=yes
    IPV4_FAILURE_FATAL=no
    IPV6INIT=yes
    IPV6_AUTOCONF=yes
    IPV6_DEFROUTE=yes
    IPV6_PEERDNS=yes
    IPV6_PEERROUTES=yes
    IPV6_FAILURE_FATAL=no
    NAME=p2p1
    UUID=7622e20e-3f2a-4b5c-83d8-f4f6e22ed7ec
    ONBOOT=yes
    HWADDR=00:14:85:BC:1C:63
    IPADDR=192.168.1.10
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1
    DNS1=127.0.0.1
    DNS2=8.8.8.8
    DNS3=8.8.4.4
