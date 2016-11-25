.. _reference-linux-contar_lineas_proyecto:

############################
Contar lineas de un proyecto
############################

**Fuentes**

* https://github.com/AlDanial/cloc
* http://stackoverflow.com/questions/26881441/can-you-get-the-number-of-lines-of-code-from-a-github-repository

----

cloc
****

.. code-block:: bash

    dnf install cloc

Para contar un proyecto en **Git** se puede usar este script (ya que un proyecto alojado, se omite
todo lo que uno no ha hecho).

.. code-block:: bash

    vim cloc-git

.. code-block:: bash

    #!/usr/bin/env bash

    git clone --depth 1 "$1" temp-linecount-repo &&
    printf "('temp-linecount-repo' will be deleted automatically)\n\n\n" &&
    cloc temp-linecount-repo &&

    rm -rf temp-linecount-repo

.. code-block:: bash

    chmod +x cloc-git
    sudo mv cloc-git /usr/local/bin

Ejemplo:

.. code-block:: bash

    cloc-git git@gitlab.com:snicoper/proyecto.git
