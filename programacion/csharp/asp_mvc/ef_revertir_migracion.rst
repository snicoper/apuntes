.. _reference-programacion-asp_mvc-ef_revertir_migracion:

#####################
EF revertir migración
#####################

.. code-block:: bash

    Update-Database -TargetMigration: $NombreMigracion

Ejecutaras todos los métodos ``Down`` de los archivos de migración, excepto ``NombreMigracion``.

Para vaciar todas las migraciones:

.. code-block:: bash

    Update-Database -TargetMigration: 0
