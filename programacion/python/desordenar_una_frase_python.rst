.. _reference-programacion-python-desordenar_una_frase_python:

####################
Desordenar un string
####################

.. code-block:: python

    import random

    tamano = 10

    abecedario = 'abcdefghijklmopqrstuvwxyz'
    desordenar = random.sample(abecedario, tamano)
    palabra = ''.join(desordenar)
    print(palabra)
