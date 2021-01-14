.. _reference--windows-install_posh_git:

#################
Instalar Posh-Git
#################

* https://github.com/dahlbyk/posh-git
* https://docs.microsoft.com/es-es/windows/terminal/tutorials/powerline-setup

Abrir ``PowerShell``

.. code-block:: bash

    Install-Module posh-git -Scope CurrentUser
    Install-Module oh-my-posh -Scope CurrentUser
    Install-Module -Name PSReadLine -Scope CurrentUser -Force -SkipPublisherCheck

.. code-block:: bash

    code $profile.CurrentUserCurrentHost

.. code-block:: bash

    Import-Module posh-git
    Import-Module oh-my-posh
    Set-Theme Paradox

Descargar fuentes: https://github.com/microsoft/cascadia-code/releases

Editar la configuración de perfil y añadir ``"fontFace": "Cascadia Code PL"``

.. code-block:: bash

    {
        // Make changes here to the powershell.exe profile.
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "Windows PowerShell",
        "commandline": "powershell.exe",
        "fontFace": "Cascadia Code PL",
        "hidden": false
    },
