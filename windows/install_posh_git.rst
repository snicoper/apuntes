.. _reference--windows-install_posh_git:

#################
Instalar Posh-Git
#################

* https://github.com/dahlbyk/posh-git

Abrir ``PowerShell``

.. code-block:: bash

    Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Confirm
    PowerShellGet\Install-Module posh-git -Scope CurrentUser
    Update-Module posh-git

    code $profile.CurrentUserCurrentHost

.. code-block:: bash

    Import-Module posh-git
    $GitPromptSettings.DefaultPromptSuffix = '`n$(''>'' * ($nestedPromptLevel + 1)) '
    $GitPromptSettings.DefaultPromptAbbreviateHomeDirectory = $true
