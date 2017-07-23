.. _reference-git-gitconfig_linux:

###################
Git Config Linux
###################

Nota, ahora al usar los `dotfiles` estos lo mismo estan obsoletos pero los dejo
por **Kdiff3**

.. code-block:: bash

    vim ~/.gitconfig

Configuración con Meld
**********************

.. code-block:: bash

    [user]
        name = Salvador Nicolas
        email = snicoper@gmail.com
    [color]
        ui = true
    [core]
        editor = vim
    [alias]
        lg = log --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr %an)%Creset' --abbrev-commit --date=relative
        co = checkout
        cm = commit
        st = status
        br = branch
    [merge]
        tool = meld
    [diff]
        tool = meld
    [mergetool]
        prompt = false
        keepBackup = false
        trustExitCode = false
        keepTemporaries = false
    [push]
        default = simple

Configuracion con Kdiff3
************************

.. code-block:: bash

    [user]
        name = Salvador Nicolas
        email = snicoper@gmail.com
    [color]
        ui = true
    [core]
        editor = vim
    [alias]
        lg = log --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr %an)%Creset' --abbrev-commit --date=relative
        co = checkout
        cm = commit
        st = status
        br = branch
    [merge]
        tool = kdiff3
    [diff]
        tool = kdiff3
    [mergetool]
        prompt = false
        keepBackup = false
        trustExitCode = false
        keepTemporaries = false
    [push]
        default = simple
