.. _reference-programacion-python-django-unittest_error_MessageMiddleware:

#####################################################################################
Unit Test Solucion para el error django.contrib.messages.middleware.MessageMiddleware
#####################################################################################

**Fuentes**

* http://stackoverflow.com/questions/11938164/why-dont-my-django-unittests-know-that-messagemiddleware-is-installed

----

.. code-block:: bash

    raise MessageFailure('You cannot add messages without installing '
    django.contrib.messages.api.MessageFailure: You cannot add messages without 
    installing django.contrib.messages.middleware.MessageMiddleware

Cuando en la view crea un ``django.contrib.messages``, con en UnitTest me da
un error cuando accedo con ``RequestFactory``, para solucionarlo.

.. code-block:: python

    from django.contrib.messages.storage.fallback import FallbackStorage
    setattr(request, 'session', 'session')
    messages = FallbackStorage(request)
    setattr(request, '_messages', messages)
    
Ejemplo mas largo.

.. code-block:: python

    def test_send_mail(self):
        """
        Manda un email cuando se ha completado el
        formulario.
        """
        form_data = {
            'email': 'test@example.com',
            'subject': 'test subject',
            'message': 'test test test'
        }
        request = self.factoty.post(reverse('contact.contact'), data=form_data)
        # http://stackoverflow.com/questions/11938164/
        # why-dont-my-django-unittests-know-that-messagemiddleware-is-installed
        from django.contrib.messages.storage.fallback import FallbackStorage
        setattr(request, 'session', 'session')
        messages = FallbackStorage(request)
        setattr(request, '_messages', messages)
        # ----- #
        request.user = self.user
        ContactView.as_view()(request)
        self.assertEqual(len(mail.outbox), 1)
    
