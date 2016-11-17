.. _reference-linux-crear_grupos_anadir_usuarios_a_grupo:

#######################################
Crear grupos y añadir usuarios a grupos
#######################################

Crear un grupo

.. code-block:: bash

    goupadd nombre_grupo

Crear un usuario que pertenezca a un grupo, entre () es un ejemplo.

.. code-block:: bash

    adduser -c "Comentario (Git users)" -g nombre_grupo (git) nombre_usuario
    passwd nombre_usuario

Otra manera de añadir a un usuario seria

.. code-block:: bash

    adduser nombre_usuario
    passwd nombre_usuario
    usermod -a -G nombre_grupo nombre_usuario
