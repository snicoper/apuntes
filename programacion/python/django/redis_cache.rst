.. _reference-programacion-python-django-redis_cache:

###########
Redis Cache
###########

:ref:`reference-linux-redis-instalar_redis`.

.. code-block:: bash

    pip install django-redis


Configuración en ``settings.py``

.. code-block:: python

    # Redis CACHE
    CACHES = {
        "default": {
            "BACKEND": "django_redis.cache.RedisCache",
            "LOCATION": "redis://127.0.0.1:6379/1",
            "OPTIONS": {
                "CLIENT_CLASS": "django_redis.client.DefaultClient",
            }
        }
    }

    # Poner sessions con redis
    SESSION_ENGINE = "django.contrib.sessions.backends.cache"
    SESSION_CACHE_ALIAS = "default"
