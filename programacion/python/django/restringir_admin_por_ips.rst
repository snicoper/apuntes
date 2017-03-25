.. _reference-programacion-python-django-restringir_admin_por_ips:

########################
Restringir admin por IPs
########################

**Fuentes**

* https://djangosnippets.org/snippets/2095/

---

.. code-block:: python

    from django.conf import settings
    from django.http import Http404
    from django.urls import reverse, NoReverseMatch


    class InternalUseOnlyMiddleware(object):
        """Middleware to prevent access to the admin if the user IP isn't in the
        INTERNAL_IPS setting.
        """

        def process_request(self, request):
            try:
                admin_index = reverse('admin:index')
            except NoReverseMatch:
                return
            if not request.path.startswith(admin_index):
                return
            remote_addr = request.META.get(
                'HTTP_X_REAL_IP', request.META.get('REMOTE_ADDR', None)
            )
            if remote_addr not in settings.INTERNAL_IPS and not settings.DEBUG:
                raise Http404



Otra opción, ver configuración de Nginx (:ref:`reference-linux-nginx-restringir_url_ip`)
