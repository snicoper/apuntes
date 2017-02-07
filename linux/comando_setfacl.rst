.. _reference-linux-comando_setfacl:

###############
Comando setfacl
###############

Para poder compartir permisos con 2 usuarios distintos, usar setfacl
Por ejemplo, en el directorio /home/snicoper/public_html/example.com/uploads

.. code-block:: bash

    sudo setfacl -R -m u:snicoper:rwx -m u:apache:rwx ~/public_html/example.com/uploads
    sudo setfacl -dR -m u:snicoper:rwx -m u:apache:rwx ~/public_html/example.com/uploads

De esta manera, tanto apache como snicoper, tendrán permisos rwx

