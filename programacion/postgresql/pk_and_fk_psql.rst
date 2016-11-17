.. _reference-programacion-postgresql-pk_and_fk_psql:

####################
PK, FK y UNIQUE Psql
####################

Fuentes
*******

* http://www.postgresql.org/docs/9.3/static/ddl-constraints.html

-------

.. code-block:: sql

    create table usuarios(
        id SERIAL,
        nombre VARCHAR(50) NOT NULL,
        password VARCHAR(40),

        CONSTRAINT pk_usuarios PRIMARY KEY(id)
    );

    create table tablon_anuncios(
        id SERIAL,
        id_usuario INT NOT NULL,
        fecha INT NOT NULL DEFAULT EXTRACT(epoch from now()),
        titulo VARCHAR(255) NOT NULL,
        contenido text NOT NULL,
        CONSTRAINT pk_tablon_anuncios PRIMARY KEY(id_usuario),
        CONSTRAINT fk1_tablon_anuncios FOREIGN KEY(id_usuario)
            REFERENCES usuarios(id) MATCH SIMPLE
            ON UPDATE CASCADE ON DELETE CASCADE
    );

    -- Crea la clave primaria de la tabla
    CONSTRAINT pk_tablon_anuncios PRIMARY KEY(id_usuario),

    -- Le dice, que la col id_usuario de la tabla tablon_anuncios
    -- es la foreign key, que usa como referencia la tabla usuarios
    -- col id
    CONSTRAINT fk1_tablon_anuncios FOREIGN KEY(id_usuario)
        REFERENCES usuarios(id) MATCH SIMPLE
        ON UPDATE CASCADE ON DELETE CASCADE

    -- unique
    CONSTRAINT unq_tablon_anuncios UNIQUE(nombre_tabla)
