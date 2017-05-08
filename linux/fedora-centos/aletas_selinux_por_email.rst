.. _reference-linux-fedora-centos-aletas_selinux_por_email:

################################
Enviar alertas SELinux por email
################################

**Fuentes**

* http://major.io/2011/09/15/receive-e-mail-reports-for-selinux-avc-denials/

-----

.. code-block:: bash

    # Centos
    yum install setroubleshoot{-server,-plugins}

El archivo de configuración esta en: ``/etc/setroubleshoot/setroubleshoot.conf``,
lo dejo todo por defecto.

.. code-block:: bash

    echo "selinux@mycompany.com" >> /var/lib/setroubleshoot/email_alert_recipients

.. code-block:: bash

    service messagebus restart

Para probarlo, cambiar el puerto de ``ssh`` y conectar.
