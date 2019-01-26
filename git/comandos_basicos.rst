.. _reference-git-comandos_basicos:

####################
Comandos Básicos Git
####################

Links
*****

* http://www.maefloresta.com/portal/es/git.es

.. note::
    Es una recopilación que voy encontrando, generalmente son cosas simples.

Comandos Básicos
****************

Creación de un repositorio.

.. code-block:: bash

    git init .

Clonar un repositorio.

.. code-block:: bash

    git clone url

Añade un directorio de manera recursiva, o un archivo para que sea
incluido en el próximo commit.

.. code-block:: bash

    git add nombre

Añade todos los archivos para que sea incluido en el próximo commit.

.. code-block:: bash

    git add --all

    # También
    git add .

Eliminar un archivo o directorio de manera recursiva.

.. code-block:: bash

    git rm nombre

Mover archivo o directorio a una nueva ruta.

.. code-block:: bash

    # -f : Sobre-escribe los cambios locales no guardados
    git mv nombre

Imprime un reporte del estado actual del árbol de trabajo local.

.. code-block:: bash

    # git st, por el alias
    git status

Muestra la diferencia entre los cambios en el árbol de trabajo local.

.. code-block:: bash

    git diff ruta

Muestra las diferencias entre los cambios registrados y los no registrados.

.. code-block:: bash

    git diff HEAD ruta

Marca el archivo para que no sea incluido en el próximo commit.

.. code-block:: bash

    git reset HEAD ruta

Realiza el commit de los archivos que han sido registrados (con git-add)

.. code-block:: bash

    -a : Automáticamente registra todos los archivos modificados.
    -m 'Texto del commit aquí' : Añade automáticamente el commit con el comentario.
    git commit

Deshace commit & conserva los cambios en el árbol de trabajo local.

.. code-block:: bash

    git reset --soft HEAD^

Restablece el árbol de trabajo local a la versión del ultimo commit.

.. code-block:: bash

    git reset --hard HEAD^

Elimina archivos desconocidos del árbol de trabajo local.

.. code-block:: bash

    git clean

Muestra el log del commit, opcionalmente de la ruta especifica.

.. code-block:: bash

    git log [ruta]

Trae los cambios desde un repositorio remoto.

.. code-block:: bash

    git fetch [remote]

Descarga y guarda los cambios realizados desde un repositorio remoto.

.. code-block:: bash

    git pull [remote]

Guarda los cambios en un repositorio remoto.

.. code-block:: bash

    git push [remote]

Lista los repositorios remotos.

.. code-block:: bash

    git remote

Añade un repositorio remoto a la lista de repositorios registrados.

.. code-block:: bash

    git remote add remote url

Cambia el árbol de trabajo local a la rama indicada.

.. code-block:: bash

    # -b rama : Crea la rama antes de cambiar el árbol de trabajo local a dicha rama.
    git checkout rama

Lista las ramas locales.

.. code-block:: bash

    git branch

Lista las ramas remotas.

.. code-block:: bash

    git branch -r

Eliminar un branch.

.. code-block:: bash

    git branch -d branch

Eliminar un branch

Sobre-escribe la rama existente y comienza desde la revisión.

.. code-block:: bash

    git branch -f rama rev

Guarda los cambios desde la rama.

.. code-block:: bash

    git merge rama

un tracker files

.. code-block:: bash

    git rm -r --cached <your directory>

git flow
********

Inicializar git flow

.. code-block:: bash

    git flow init

Crear una feature

.. code-block:: bash

    git flow feature start nombre_feature

Subir feature

.. code-block:: bash

    git push origin feature/nombre_feature

Obtener feature

.. code-block:: bash

    git pull origin feature/nombre_feature

Finalizar feature

.. code-block:: bash

    git flow feature finish nombre_feature

Eliminar branch remota

.. code-block:: bash

    git push origin --delete feature/nombre_feature
