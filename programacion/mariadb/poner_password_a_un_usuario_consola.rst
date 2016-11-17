.. _reference-programacion-mariadb-poner_password_a_un_usuario_consola:

############################################
Poner password a un usuario desde la consola
############################################

.. code-block:: sql

    SET PASSWORD FOR 'user'@'localhost' = PASSWORD('pass');

Otra manera ya que los passwords y usuarios están en la tabla mysql.user seria

.. code-block:: sql

    UPDATE user
        SET user.Password = PASSWORD('123456')
        WHERE user.Host = 'localhost'
        AND user.User = 'nico';

Siempre y cuando el user sea nico y el host localhost

Para ver todos los usuarios, host y si alguien no tiene pass:

.. code-block:: sql

    SELECT user.User, user.Host, user.Password
        FROM user;
