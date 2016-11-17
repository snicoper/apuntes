.. _reference--windows-instalacion_python_windows:

#############################
Instalación Python en Windows
#############################

Variables de entorno
********************

.. code-block:: bash

    C:\Python35\;C:\Python35\Scripts\;

Virtualenvwrapper
*****************

.. code-block:: sh

    pip install virtualenvwrapper-win

Por defecto usara ~/Envs para los entornos virtuales, si se quiere cambiar el directorio, añadir la variable de entorno ``WORKON_HOME`` indicandole la nueva ruta.

Añadir la variable de entorno ``WORKON_HOME`` con el valor ``%USERPROFILE%\virtualenvs``

Pysopg2
=======

``version 2.6 x64``

.. code-block:: bash

    (default) easy_install http://www.stickpeople.com/projects/python/win-psycopg/2.6.2/psycopg2-2.6.2.win-amd64-py3.5-pg9.5.3-release.exe
