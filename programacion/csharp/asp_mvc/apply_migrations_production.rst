.. _reference-programacion-asp_mvc-apply_migrations_production:

#########################################
EF6 Migraciones en servidor de producción
#########################################

**Fuentes**

* https://stackoverflow.com/a/19160290

-----------

.. warning:: Siempre crear **Backups**

.. note:: Si se puede, copiar en **producción** la tabla ``dbo._MigrationHistory``
    (todos los **SQL** que genera) para tener una referencia del estado en **producción**.

Para aplicar **migraciones** en **producción**, una manera que he encontrado es generando
``Update-Database -Script`` desde el entorno de desarrollo.

.. note:: Con ``-Script`` siempre mostrara el **SQL**, no ejecuta las sentencias en la base de datos.

Cada vez que se hace un cambio en el modelo, se ha de crear una migración con
``Add-Migration NombreMigracion`` que genera un archivo en ``~/Migrations/fecha_NombreMigracion.cs``.

Una manera de obtener el **SQL** con los cambios en ``Update-Database -Script``, pudiendo ver lo que
va a ejecutar en la base de datos (ejecutara todos los archivos de migración pendiente, es decir
los que no tenga registrados en la tabla ``dbo._MigrationHistory``).

Copiando el **SQL** del script generado y luego en **producción** ejecutarlo.

Cuando en **desarrollo** se han ejecutado todas las migraciones, para obtener los cambios de la
base de datos, se ha de ejecutar una combinación de banderas.

Imaginando que se tienen 5 migraciones, por orden de fecha:

.. code-block:: bash

    fecha_Initial.cs
    fecha_Segunda.cs
    fecha_Tercera.cs
    fecha_Cuarta.cs
    fecha_Quinta.cs

La base de datos en **producción** tiene ``fecha_Initial``, ``fecha_Segunda`` y ``fecha_Tercera`` y
en **desarrollo** todas.

Para obtener el **SQL** de ``fecha_Cuarta`` y ``fecha_Quinta`` se han de revertir los cambios se
utiliza una combinación de ``-SourceMigration`` y ``-TargetMigration``.

.. code-block:: bash

    Update-Database -Script -SourceMigration: Tercera -TargetMigration: Quinta

Se pone en ``-SourceMigration`` la ultima migración del servidor de ``producción`` y en
``-TargetMigration`` la ultima migración. De esta manera se obtiene todo el **SQL** que se deberá
aplicar al servidor de **producción**.
