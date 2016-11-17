.. _reference-git-remote_diff_and_merge:

#############################
Hacer diff y merge con remote
#############################

Primero hay que obtener las diferencias

.. code-block:: bash

    git fetch origin
    
y ahora ver las diferencias.

.. code-block:: bash

    git difftool origin/master
   
Ahora hay que hacer **merge**, se puede usar ``merge`` o ``mergetool``

