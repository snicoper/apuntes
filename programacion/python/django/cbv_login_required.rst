.. _reference-programacion-python-django-cbv_login_required:

##################
CBV login_required
##################

A partir de Django 1.9
**********************

.. code-block:: python

    # views.py
    from django.contrib.auth.mixins import LoginRequiredMixin
    from django.views import generic

    class UpdateContactView(LoginRequiredMixin, generic.UpdateView):
        pass

Antes de Django 1.9
*******************

.. code-block:: python

    from django.contrib.auth.decorators import login_required
    from django.utils.decorators import method_decorator
    from django.views import generic


    class LoggedInMixin(object):

        @method_decorator(login_required)
        def dispatch(self, *args, **kwargs):
            return super(LoggedInMixin, self).dispatch(*args, **kwargs)

    # views.py
    class UpdateContactView(LoggedInMixin, generic.UpdateView):
        pass

Tambien puede interesar `django-braces <https://github.com/brack3t/django-braces>`_
