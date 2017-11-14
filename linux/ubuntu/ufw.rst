.. _reference-linux-ubuntu-ufw:

###
ufw
###

Fuentes
*******

* https://help.ubuntu.com/14.04/serverguide/firewall.html

-----------

Estos son comandos muy básicos, para mas info en Fuentes

Habilitar

.. code-block:: bash

    sudo ufw enable

Para ver las reglas actuales

.. code-block:: bash

    sudo ufw status numbered

Para abrir un puerto

.. code-block:: bash

    sudo ufw allow 22

Cerrar un puerto

.. code-block:: bash

    sudo ufw deny 22

Para eliminar una regla

.. code-block:: bash

    sudo ufw delete deny 22
    sudo ufw delete allow 22
    sudo ufw delete allow proto tcp from 192.168.1.0/24 to any port 22

Es insertar lo mismo pero con delete después de 'sudo ufw delete (comando que se añadió)'

.. code-block:: bash

    sudo ufw allow proto tcp from 192.168.1.2 to any port 22
    sudo ufw allow proto tcp from 192.168.1.0/24 to any port 22

Abrir todo el trafico la red local

.. code-block:: bash

    sudo ufw allow from 192.168.1.0/24
