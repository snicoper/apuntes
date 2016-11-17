.. _reference-programacion-python-hashlib_python:

#######
hashlib
#######

Fuentes
*******

* https://docs.python.org/3.4/library/hashlib.html

---------


Ejemplo rapido

.. code-block:: python

    from hashlib import sha256
    a = sha256()
    a.update(b'123456')
    password = a.hexdigest()

    # Si el password es pasado en una variable
    mi_password = '123456'
    a = sha256()
    a.update(mi_password.encode('utf-8'))
    password = a.hexdigest()


