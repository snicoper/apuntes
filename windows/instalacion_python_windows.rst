.. _reference--windows-instalacion_python_windows:

#############################
Instalación Python en Windows
#############################

* https://www.python.org/

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