.. _reference-programacion-python-django-generat_token:

################
Generar un Token
################

``django.utils.crypto.get_random_string``

.. code-block:: python

    from django.utils.crypto import get_random_string

    token = get_random_string(length=30)

Argumentos por defecto:

* ``length=12``
* ``allowed_chars='abcdefghijklmnopqrstuvwxyz' 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'``

Otra opción

.. code-block:: python

    import hashlib
    import random


    def generate_token(length=12):
    """Genera un token único de 30 caracteres como máximo."""
    chars = list(
        'ABCDEFGHIJKLMNOPQRSTUVWYZabcdefghijklmnopqrstuvwyz01234567890'
    )
    random.shuffle(chars)
    chars = ''.join(chars)
    sha1 = hashlib.sha1(chars.encode('utf8'))
    token = sha1.hexdigest()
    return token[:length]

Otra opción

.. code-block:: python

    import uuid


    def generate_token():
    """Genera un token unico de 32 caracteres."""
    return str(uuid.uuid4()).replace('-', '')
