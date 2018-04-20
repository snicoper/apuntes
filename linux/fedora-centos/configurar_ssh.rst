.. _reference-linux-fedora-centos-configurar_ssh:

##############
Configurar SSH
##############

**Fuentes**

* http://www.snicoper.com/blog/article/configuracion-ssh-en-centos-7/

----

Configuración básica de ``SSH``

.. code-block:: bash

    dnf install ssh

    systemctl start sshd.service
    systemctl enable sshd.service

Editamos el archivo de configuración de ssh.

.. code-block:: bash

    vim /etc/ssh/sshd_config

.. code-block:: bash

    # Puerto
    # Linea 17, descomentar y cambiar puerto por defecto
    Port 50022

    # Permitir login con root?
    # line 38: uncomment and change 'no'
    PermitRootLogin no

    # line 64: uncomment
    PermitEmptyPasswords no

    # Disable password authentication forcing use of keys
    # line 65:
    PasswordAuthentication yes

    # Usuarios a los que se les permite conectarse
    # Añadir al final
    AllowUsers usuario1 usuario2 usuarioX

Crear una clave rsa, desde el cliente/clientes

.. code-block:: bash

    ssh-keygen -t rsa -b 4096

    # Agregar clave SSH al agente ssh (evitar tener que poner el passphrase siempre)
    ssh-add

Si ``ssh-add`` devuelve **Could not open a connection to your authentication agent.**

.. code-block:: bash

    eval `ssh-agent -s`
    ssh-add

Subirla al servidor

.. code-block:: bash

    scp .ssh/id_rsa.pub usuario@SERVER_IP_ADDRESS:

O también es posible insertarla con ``ssh-copy-id``

.. code-block:: bash

    ssh-copy-id usuario@SERVER_IP_ADDRESS
    ssh-copy-id -p PUERTO usuario@SERVER_IP_ADDRESS

En el servidor, como **usuario**

.. code-block:: bash

    mkdir .ssh
    chmod 700 .ssh
    touch .ssh/authorized_keys
    chmod 600 .ssh/authorized_keys
    cat id_rsa.pub > .ssh/authorized_keys

Firewalld
*********

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=ssh

    # Si es un puerto distinto al 22
    firewall-cmd --permanent --zone=public --add-port=puerto/tcp
    firewall-cmd --reload

SELinux
*******

Si es un puerto distinto al 22

.. code-block:: bash

    semanage port -a -t ssh_port_t -p tcp PUERTO_NUEVO

Si se ha cambiado el puerto, para entrar con ``ssh``

.. code-block:: bash

    ssh -p PUERTO usuario@SERVER_IP_ADDRESS
