.. _reference-programacion-python-django-login_username_or_email:

##########################
Login con username o email
##########################

Con este pequeño tip, vamos a permitir que un usuario pueda loguearse poniendo el email y/o username
y contraseña.

En el archivo de configuración ``settings.py`` vamos a crear una variable ``AUTH_AUTHENTICATION_TYPE``
con uno de los siguientes valores: ``both``, ``email``, ``username``.

Ademas, tenemos que cambiar el valor de ``AUTHENTICATION_BACKENDS``. El valor es una lista o tupla
con los backends de autenticación, valga la redundancia.

``settings.py``

.. code-block:: python

    AUTH_AUTHENTICATION_TYPE = 'both'

    AUTHENTICATION_BACKENDS = (
    'accounts.backends.EmailOrUsernameModelBackend',
    )

Se entiende que tenemos la app ``accounts`` y dentro de ella, creamos el archivo ``backends.py``.

Dentro de ``backends.py`` añadimos:

.. code-block:: python

    from django.conf import settings
    from django.contrib.auth import get_user_model
    from django.contrib.auth.backends import ModelBackend
    from django.db.models import Q


    class EmailOrUsernameModelBackend(ModelBackend):

        def authenticate(self, username=None, password=None):
            auth_type = settings.AUTH_AUTHENTICATION_TYPE
            if auth_type == 'username':
                return super().authenticate(username, password)
            user_model = get_user_model()
            try:
                if auth_type == 'both':
                    user = user_model.objects.get(
                        Q(username__iexact=username) | Q(email__iexact=username)
                    )
                else:
                    user = user_model.objects.get(email__iexact=username)
                if user.check_password(password):
                    return user
            except user_model.DoesNotExist:
                return None

Ahora iniciando el servidor, puedes jugar un poco y ver los resultados http://127.0.0.1:8000/admin/
