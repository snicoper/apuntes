.. _reference-git-unstage:

#########################
Unstage file or directory
#########################

**Fuentes**

* http://stackoverflow.com/questions/6919121/why-are-there-2-ways-to-unstage-a-file-in-git

-------

Para hacer unstaging de un archivo o directorio

.. code-block:: bash

    git rm --cached ruta/file/or/dir

``git rm --cached`` se utiliza para eliminar un archivo del índice. En el caso de que el archivo ya
está en el repositorio, ``git rm --cached`` eliminará el archivo del índice, dejándolo en el
directorio de trabajo.
