.. _reference-linux-php-phpdocumentor:

###############
PHPDocumentor 2
###############

PHAR
====

Como root

.. code-block:: bash

    wget http://phpdoc.org/phpDocumentor.phar
    chmod +x phpDocumentor.phar
    mv phpDocumentor.phar /usr/local/bin/phpdoc
    phpdoc --version

PEAR
====

Instalar :ref:`reference-linux-php-pear`

.. code-block:: bash

    pear channel-discover pear.phpdoc.org
    pear install phpdoc/phpDocumentor

Composer
========

Instalar :ref:`reference-linux-php-composer`

.. code-block:: bash

    composer require --dev phpdocumentor/phpdocumentor dev-master

Después se podrá ejecutar phpDocumentor directamente desde el directorio ``vendor``:
