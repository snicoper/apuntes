.. _reference-programacion-python-django-django_signals:

##############
Django signals
##############

**Referencias**

* https://docs.djangoproject.com/en/1.8/ref/signals/
* http://www.koopman.me/2015/01/django-signals-example/
* http://www.snicoper.com/blog/article/signals-en-django/

----

Para un pequeño ejemplo, vamos a crear un modelo ``UserProfile`` con la información
del usuario. Vamos a añadir los campos ``pais`` y ``provincia`` y un campo ``user``
que tendrá una relación ``OneToOneField`` con ``settings.AUTH_USER_MODEL``.

En este caso, se supone que se usara después de que el usuario haya sido creado,
pero no la mostrara en el formulario de registro, por eso, los campos ``pais`` y
``provincia`` serán ``default='', blank=True`` (``blank=True``, ya va a gustos
si cuando muestre el formulario, es requerido o no).

.. code-block:: python

    # accounts/models.py
    from django.db import models
    from django.conf import settings


    class UserProfile(models.Model):
        user = models.OneToOneField(
            settings.AUTH_USER_MODEL, primary_key=True, related_name='user_profile'
        )
        pais = models.CharField(max_length=100, default='', blank=True)
        provincia = models.CharField(max_length=100, default='', blank=True)
        # Otros campos...

Ahora, podemos hacelo de dos maneras, una añadiendo el **signal** en el mismo
modulo del modelo, o bien creando un modulo separado ``signals.py``.

Para crearlo en el mismo modulo ``models.py``, creamos el **signal** abajo del
archivo.

.. code-block:: python

    # accounts/models.py
    # Importar los módulos necesarios al principio.
    from django.db.models.signals import post_save
    from django.dispatch import receiver
    from django.conf import settings


    @receiver(post_save, sender=settings.AUTH_USER_MODEL)
    def create_profile_handler(sender, instance, created, **kwargs):
        if not created:
            return
        UserProfile.objects.create(user=instance)

Cada vez que se cree, un usuario, se creara un campo en el modelo UserProfile.
Esta es la manera rápido, pero si hay muchos **signals** lo ideal es ponerlos
todos juntos en el modulo ``signals``.

.. code-block:: python

    # accounts/signals.py
    from django.db.models.signals import post_save
    from django.dispatch import receiver
    from django.conf import settings

    @receiver(post_save, sender=settings.AUTH_USER_MODEL)
    def create_profile_handler(sender, instance, created, **kwargs):
        if not created:
            return
        UserProfile.objects.create(user=instance)

De momento, no hemos hecho nada nuevo..., creamos un modulo ``apps.py`` y añadimos.

.. code-block:: python

    # accounts/apps.py
    from django.apps import AppConfig


    class AccountsConfig(AppConfig):
        name = 'accounts'
        verbose_name = 'Accounts Application'

        def ready(self):
            from . import signals

Donde ``name = 'accounts'`` es la ruta a la app, si estuviera en ``apps/accounts``,
se tendria que cambiar por ``name = 'apps.accounts'``, ``verbose_name`` es un
nombre legible que le damos.

Con esto, cada vez que se cree un nuevo usuario en la base de datos, se creara
una fila en la table ``accounts_userprofile`` con un campo relacional a
``auth_user`` (por defecto).
