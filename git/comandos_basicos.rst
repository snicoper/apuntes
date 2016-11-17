.. _reference-git-comandos_basicos:

####################
Comandos Basicos Git
####################

Links
*****

* http://www.maefloresta.com/portal/es/git.es

.. note::
    Es una recopilación que voy encontrando, generalmente son cosas simples.

Comandos Basicos
****************

Creacion de un repositorio.

.. code-block:: none

    git init .

Clonar un repositorio.

.. code-block:: none

    git clone url

Añade un directorio de manera recursiva, o un archivo para que sea
incluido en el próximo commit.

.. code-block:: none

    git add nombre

Añade todos los archivos para que sea incluido en el próximo commit.

.. code-block:: none

    git add --all

Eliminar un archivo o directorio de manera recursiva.

.. code-block:: none

    git rm nombre

Mover archivo o directorio a una nueva ruta.

.. code-block:: none

    # -f : Sobre-escribe los cambios locales no guardados
    git mv nombre

Imprime un reporte del estado actual del árbol de trabajo local.

.. code-block:: none

    # git st, por el alias
    git status

Muestra la diferencia entre los cambios en el árbol de trabajo local.

.. code-block:: none

    git diff ruta

Muestra las diferencias entre los cambios registrados y los no registrados.

.. code-block:: none

    git diff HEAD ruta

Marca el archivo para que no sea incluido en el próximo commit.

.. code-block:: none

    git reset HEAD ruta

Realiza el commit de los archivos que han sido registrados (con git-add)

.. code-block:: none

    -a : Automáticamente registra todos los archivos modificados.
    -m 'Texto del commit aqui' : Añade automaticamente el commit con el comentario.
    git commit

Deshace commit & conserva los cambios en el árbol de trabajo local.

.. code-block:: none

    git reset --soft HEAD^

Restablece el árbol de trabajo local a la versión del ultimo commit.

.. code-block:: none

    git reset --hard HEAD^

Elimina archivos desconocidos del árbol de trabajo local.

.. code-block:: none

    git clean

Muestra el log del commit, opcionalmente de la ruta especifica.

.. code-block:: none

    git log [ruta]

Trae los cambios desde un repositorio remoto.

.. code-block:: none

    git fetch [remote]

Descarga y guarda los cambios realizados desde un repositorio remoto.

.. code-block:: none

    git pull [remote]

Guarda los cambios en un repositorio remoto.

.. code-block:: none

    git push [remote]

Lista los repositorios remotos.

.. code-block:: none

    git remote

Añade un repositorio remoto a la lista de repositorios registrados.

.. code-block:: none

    git remote add remote url

Cambia el árbol de trabajo local a la rama indicada.

.. code-block:: none

    # -b rama : Crea la rama antes de cambiar el árbol de trabajo local a dicha rama.
    git checkout rama

Lista las ramas locales.

.. code-block:: none

    git branch

Eliminar un brach.

.. code-block:: none

    git brach -d brach

Sobre-escribe la rama existente y comienza desde la revisión.

.. code-block:: none

    git branch -f rama rev

Guarda los cambios desde la rama.

.. code-block:: none

    git merge rama

untacker files

.. code-block:: none

    git rm -r --cached <your directory>

