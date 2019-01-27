.. _reference-linux-fedora-centos-reglas_selinux:

##############
Reglas SELinux
##############

Virt-Manager y Boxes (Cajas)
****************************

.. code-block:: bash

    setsebool -P virt_use_fusefs 1
    setsebool -P virt_use_rawip 1

Bind
****

.. code-block:: bash

    setsebool -P named_write_master_zones 1

Postfix
*******
Para permitir a Apache poder enviar correo electrónico desde alguna aplicación

.. code-block:: bash

    setsebool -P httpd_can_sendmail 1
    setsebool -P httpd_read_user_content 1
    setsebool -P httpd_can_network_connect 1

Postgresql
**********

.. code-block:: bash

    setsebool -P allow_user_postgresql_connect 1

Memcached
*********

.. code-block:: bash

    setsebool -P httpd_can_network_memcache 1

Apache2.4 y Nginx
*****************

Para permitir que Apache/Nginx pueda leer contenidos localizados en los directorios
de los usuarios.

.. code-block:: bash

    # setsebool -P httpd_enable_homedirs 1
    setsebool -P httpd_read_user_content 1
    setsebool -P httpd_can_network_connect 1

Para definir que un directorio fuera de ``/var/www``, como por ejemplo
``/sitios/dominio.tld/html``, pueda ser utilizado por Apache, se le debe asignar el
contexto httpd_sys_content_t. Éste puede asignarse a través del mandato chcon,
como se muestra en el siguiente ejemplo

.. code-block:: bash

    chcon -t httpd_sys_content_t /sitios/dominio.tld/htm

    # ls -Z para saber el contexto
