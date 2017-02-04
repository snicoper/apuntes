.. _reference--windows-instalacion_python_windows:

#############################
Instalación Python en Windows
#############################

Variables de entorno
********************

.. code-block:: bash

    C:\Python36\
    C:\Python36\Scripts\

Virtualenvwrapper
*****************

.. code-block:: sh

    pip install virtualenvwrapper-win

Por defecto usara ``~/Envs`` para los entornos virtuales, si se quiere cambiar el directorio,
añadir la variable de entorno ``WORKON_HOME`` indicándole la nueva ruta.

``WORKON_HOME`` con el valor ``%USERPROFILE%\virtualenvs``

Pysopg2
=======

* http://www.stickpeople.com/projects/python/win-psycopg/

**Version 2.6 x64 para Python 3.6**

.. note::

    No se si funcionara con ``Python 3.6``, ya que el de ``x64`` no saldrá hasta ``Python 3.6.1`` y el que
    dejo es para ``Python 3.5``.

.. code-block:: bash

    (myenv) easy_install http://www.stickpeople.com/projects/python/win-psycopg/2.6.2/psycopg2-2.6.2.win-amd64-py3.5-pg9.5.3-release.exe

**Version 2.6 x86 para Python 3.6**

.. code-block:: bash

    (myenv) easy_install http://www.stickpeople.com/projects/python/win-psycopg/2.6.2/psycopg2-2.6.2.win32-py3.6-pg9.6.1-release.exe
