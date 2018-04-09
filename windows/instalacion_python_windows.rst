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

Virtualenvwrapper Powershell
****************************

* https://github.com/regisf/virtualenvwrapper-powershell

Descargar repo y pegar en ``~\Documents\WindowsPowerShell\Modules``

* ``VirtualEnvWrapper.psm1``

Editar

.. code-block:: bash

    code $profile.CurrentUserCurrentHost

Añadir

.. code-block:: language

    $MyDocuments = [Environment]::GetFolderPath("mydocuments")
    Import-Module $MyDocuments\WindowsPowerShell\Modules\VirtualEnvWrapper.psm1
