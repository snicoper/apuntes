.. _reference-linux-comprimir_descomprimir_desde_consola:

####################################
Comprimir descomprimir desde consola
####################################

Ficheros tar

.. code-block:: bash

    # Empaquetar:
    tar -cvf archivo.tar /dir/a/comprimir/

    # Desempaquetar:
    tar -xvf archivo.tar

    # Ver contenido:
    tar -tf archivo.tar

Ficheros gz

.. code-block:: bash

    #Comprimir:
    gzip -9 fichero

    # Descomprimir:
    gzip -d fichero.gz

Ficheros bz2

.. code-block:: bash

    # Comprimir:
    bzip fichero

    # Descomprimir:
    bzip2 -d fichero.bz2

gzip ó bzip2 sólo comprimen ficheros [no directorios, para eso existe tar].
Para comprimir y archivar al mismo tiempo hay que combinar el tar y el gzip
o el bzip2 de la siguiente manera:

Ficheros tar.gz

.. code-block:: bash

    # Comprimir:
    tar -czfv archivo.tar.gz ficheros

    # Descomprimir:
    tar -xzvf archivo.tar.gz

    # Ver contenido:
    tar -tzf archivo.tar.gz

Ficheros tar.bz2

.. code-block:: bash

    # Comprimir:
    tar -c ficheros | bzip2 > archivo.tar.bz2

    # Descomprimir:
    bzip2 -dc archivo.tar.bz2 | tar -xv

    # Ver contenido:
    bzip2 -dc archivo.tar.bz2 | tar -t

Ficheros zip

.. code-block:: bash

    # Comprimir:
    zip archivo.zip ficheros

    # Descomprimir:
    unzip archivo.zip

    # Ver contenido:
    unzip -v archivo.zip

Ficheros lha

.. code-block:: bash

    # Comprimir:
    lha -a archivo.lha ficheros

    # Descomprimir:
    lha -x archivo.lha

    # Ver contenido:
    lha -v archivo.lha

    # Ver contenido:
    lha -l archivo.lha

Ficheros arj

.. code-block:: bash

    # Comprimir:
    arj a archivo.arj ficheros

    # Descomprimir:
    unarj archivo.arj

    # Descomprimir:
    arj -x archivo.arj

    # Ver contenido:
    arj -v archivo.arj

    # Ver contenido:
    arj -l archivo.arj

Ficheros zoo

.. code-block:: bash

    # Comprimir:
    zoo a archivo.zoo ficheros

    # Descomprimir:
    zoo -x archivo.zoo

    # Ver contenido:
    zoo -L archivo.zoo

    # Ver contenido:
    zoo -v archivo.zoo

Ficheros rar

.. code-block:: bash

    # Comprimir: rar -a archivo.rar ficheros

    # Descomprimir: rar -x archivo.rar

    # Ver contenido: rar -l archivo.rar

    # Ver contenido: rar -v archivo.rar
