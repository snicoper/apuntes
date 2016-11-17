#####################
Django Authentication
#####################

Configuraciones
===============

En ``src/config/settings/base.py``

*   ``AUTHENTICATION_TYPE``: ``both``, ``username`` o ``email``, por defecto ``both``
*   ``AUTH_REGISTER_EXPIRE_DAYS``: días antes de expirar los registros temporales por defecto ``1``

Requiere configruacion **SMTP**, cambiar valores de:

.. code-block:: python

    EMAIL_USE_TLS = True
    EMAIL_HOST = 'smtp.gmail.com'
    EMAIL_PORT = '587'
    EMAIL_HOST_USER = 'user@gmail.com'
    EMAIL_HOST_PASSWORD = 'password_gmail'

Migración e iniciar
===================

Desde un entorno virtual

.. code-block:: bash

    pip install -r requirements/local.txt

    ./manage.py migrate
    ./manage.py createsuperuser # opcional
    ./manage.py runserver

http://127.0.0.1:8000
