.. _reference-linux-nginx-rewrite_php:

###########
Rewrite PHP
###########

.. code-block:: bash

    location / {
        index index.html index.htm index.php;
        if (!-e $request_filename) {
            rewrite /(.*)$ /index.php?uri=$1 last;
            break;
        }
    }
