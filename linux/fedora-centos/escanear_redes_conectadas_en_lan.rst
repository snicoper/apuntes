.. _reference-linux-fedora-centos-escanear_redes_conectadas_en_lan:

################################
Escanear redes conectadas en Lan
################################

.. code-block:: bash

    sudo yum -y install arp-scan
    sudo arp-scan --interface=p2p1 --localnet
