.. _reference-linux-tunel_ssh:

.. |br| raw:: html

   <br />

#########
Tunel SSH
#########

.. code-block:: bash

    ssh snicoper@lxmaq1.workspace.local -L 3307:localhost:3306 -N

**3307**: Es el puerto que asigno a la maquina cliente |br|
**3306**: El puerto del host

Ahora desde el cliente

.. code-block:: bash

    mysql -h 127.0.0.1 -u root -p -P 3307
