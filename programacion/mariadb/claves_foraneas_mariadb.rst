.. _reference-programacion-mariadb-claves_foraneas_mariadb:

#######################
Claves Foráneas MariaDB
#######################

Para la creación de las claves foráneas, existen 2 tablas, una tabla padre que
es la que contiene un id único y una tabla que contiene un id que hace referencia
a la clase padre.

.. note::
    Me he dado cuenta que para que se pueda crear bien la foreign key, si la
    tabla padre la id es ``UNSIGNED`` la id hija ha de serlo también.

.. code-block:: sql

    -- Clase padre
    CREATE TABLE IF NOT EXISTS usuarios (
        id_usr INT UNSIGNED NOT NULL AUTO_INCREMENT,
        nombre_usr VARCHAR(30) NOT NULL,
        PRIMARY KEY(id_usr)
    ) ENGINE = InnoDB;

La clase hija tiene una id que hace referencia a la clase padre y no se podrá
poner una id donde no exista en la clase padre.
Las id ha de ser un tipo ``KEY/INDEX, PRIMARY KEY``, etc, en caso de
no existir a partir de MySQL 5 crea un index para las tablas.

.. code-block:: sql

    -- Clase hija
    CREATE TABLE IF NOT EXISTS comentarios (
        id_cmt INT UNSIGNED NOT NULL AUTO_INCREMENT,
        id_usr INT UNSIGNED NOT NULL,
        comentario_cmt TEXT NOT NULL,
        PRIMARY KEY(id_cmt),
        INDEX(id_usr),
        FOREIGN KEY (id_usr)
            REFERENCES usuarios(id_usr)
            ON DELETE CASCADE
            ON UPDATE NO ACTION
    ) ENGINE = InnoDB;

Las clases hijas son las que tienen la foreign key y hay dos formas de crear una
foreign key, o bien dentro de la creación de la tabla

.. code-block:: sql

    (
        FOREIGN KEY (column_id)
            REFERENCES tabla_padre(column_id)
            ON DELETE CASCADE
            ON UPDATE NO ACTION
    )

    o con ALTER TABLE:

    ALTER TABLE tabla_hija
            ADD CONSTRAINT FK_tabla_hija
            FOREIGN KEY (column_id)
            REFERENCES tabla_padre(column_id)
            ON UPDATE CASCADE
            ON DELETE RESTRICT;

Donde CASCADE hay 4 tipos:

.. code-block:: bash

    [ON DELETE {RESTRICT | CASCADE | SET NULL | NO ACTION}]
    [ON UPDATE {RESTRICT | CASCADE | SET NULL | NO ACTION}]

CASCADE:
    Borra o actualiza el registro en la tabla padre y automáticamente
    borra o actualiza los registros coincidentes en la tabla hija.
    Tanto ON DELETE CASCADE como ON UPDATE CASCADE están disponibles en MySQL 5.0.
    Entre dos tablas, no se deberían definir varias cláusulas ON UPDATE CASCADE
    que actúen en la misma columna en la tabla padre o hija.
SET NULL:
    Borra o actualiza el registro en la tabla padre y establece en NULL la o las
    columnas de clave foránea en la tabla hija. Esto solamente es válido si las
    columnas de clave foránea no han sido definidas como NOT NULL. MySQL 5.0
    soporta tanto ON DELETE SET NULL como ON UPDATE SET NULL.
NO ACTION:
    En el estándar ANSI SQL-92, NO ACTION significa ninguna acción en el sentido
    de que un intento de borrar o actualizar un valor de clave primaria no sera
    permitido si en la tabla reverenciada hay una valor de clave foránea
    relacionado. (Gruber, Mastering SQL, 2000:181). En MySQL 5.0, InnoDB rechaza
    la operación de eliminación o actualización en la tabla padre
RESTRICT:
    Rechaza la operación de eliminación o actualización en la tabla padre.
    NO ACTION y RESTRICT son similares en tanto omiten la cláusula ON DELETE
    u ON UPDATE. (Algunos sistemas de bases de datos tienen verificaciones
    diferidas o retrasadas, una de las cuales es NO ACTION. En MySQL, las
    restricciones de claves foráneas se verifican inmediatamente, por eso,
    NO ACTION y RESTRICT son equivalentes.)
SET DEFAULT:
    Esta acción es reconocida por el procesador de sentencias (parser), pero
    InnoDB rechaza definiciones de tablas que contengan ON DELETE SET DEFAULT
    u ON UPDATE SET DEFAULT.
