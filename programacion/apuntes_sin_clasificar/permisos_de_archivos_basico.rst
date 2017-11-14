.. _reference-programacion-apuntes_sin_clasificar-permisos_de_archivos_basico:

###########################
Permisos de archivos básico
###########################

.. note::
    Aunque lo apunte de un libro de php, en realidad es parte
    del sistema de Linux.

Dependiendo de los permisos, lo que repercute en archivos y directorios.

========        ===============================     ============================
Permisos        Lo que permite en un directorio     Lo que permite en un archivo
========        ===============================     ============================
read            Ver su contenido (ls)               Ver, Copiar, Imprimir, etc
write           Crear o eliminar archivos en el     Modificar, renombrar o
                directorio.                         eliminarlo.
========        ===============================     ============================

Valores numéricos para permisos de archivos para clases de usuarios

==========      ===========     =====   =====
Orden           Propietario     Grupo   Otros
==========      ===========     =====   =====
Lectura         400             040     004
Escritura       200             020     002
Ejecución       100             010     001
==========      ===========     =====   =====

Es decir un archivo con permisos 700 seria que al propietario puede leer, escribir y ejecutar, pero
el resto no podrían hacer ninguna de las cosas (-rwx------).

Se suman los valores en cada columna y se obtiene los permisos, 777 es el máximo

Para mas información leer el libro PHP y MySQL Practico para diseñadores y programadores web pagina 469

En Beginning PHP 5.3 da mas datos sobre los permisos y pone todos los números (pag 352)

| 1   No se puede leer, escribir o ejecutar el archivo
| 2   Sólo puede ejecutar el archivo
| 3   Sólo se pueden escribir en el fichero
| 4   Se puede escribir y ejecutar el archivo
| 5   Pueden leer y ejecutar el archivo
| 6   Puede leer y escribir en el fichero
| 7   Puede leer, escribir y ejecutar el archivo
|

Para dar permisos con chmod() se ha de hacer de la siguiente manera:
bool chmod('nombre_archivo.dat', 0644);
