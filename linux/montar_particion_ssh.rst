.. _reference-linux-kde-montar_particion_ssh:

#######################################
Montar partición SSH al iniciar sistema
#######################################

Fuentes
*******

* https://wiki.archlinux.org/index.php/Sshfs

Fedora
******

.. code-block:: bash

    dnf install fuse-sshfs

    vim /etc/fstab

    snicoper@192.168.1.33:/home/snicoper /run/media/snicoper/srv1 fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/snicoper/.ssh/id_rsa,allow_other,reconnect 0 0

    # Con puerto diferente a 22
    snicoper@192.168.1.33:/home/snicoper /run/media/snicoper/srv1 fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,port=22222,IdentityFile=/home/snicoper/.ssh/id_rsa,allow_other,reconnect 0 0
