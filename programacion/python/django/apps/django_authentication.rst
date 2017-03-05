#####################
Django Authentication
#####################

Configuraciones
===============

En ``src/config/settings/base.py``

*   ``AUTHENTICATION_TYPE``: ``both``, ``username`` o ``email``, por defecto ``both``
*   ``AUTH_REGISTER_EXPIRE_DAYS``: días antes de expirar los registros temporales por defecto ``1``

Requiere configuración **SMTP**, cambiar valores de:

.. code-block:: python

    EMAIL_USE_TLS = True
    EMAIL_HOST = 'smtp.gmail.com'
    EMAIL_PORT = '587'
    EMAIL_HOST_USER = 'user@gmail.com'
    EMAIL_HOST_PASSWORD = 'password_gmail'
