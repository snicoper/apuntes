.. _reference-git-git_windows:

##############
Git en Windows
##############

Instalar `Git <http://git-scm.com>`_

Añadir al path

.. code-block:: bash

    C:\Program Files\Git\bin
    C:\Program Files\Git\cmd
    C:\Program Files\Git\usr\bin

Gitconfig con kdiff3
====================

`Descargar Kdiff3 <http://kdiff3.sourceforge.net/>`_

.. code-block:: bash

    [user]
        name = Salvador Nicolas
        email = snicoper@gmail.com
    [color]
        ui = true
    [core]
        editor = vim
        autocrlf = input
	    eol = lf
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
    [mergetool "kdiff3"]
        path = C:/Program Files/KDiff3/kdiff3.exe
        prompt = false
        keepBackup = false
        trustExitCode = false
        keepTemporaries = false
    [push]
        default = simple

Gitconfig con Meld
==================

`Descargar Meld <http://meldmerge.org/>`_

.. code-block:: bash

    [user]
        name = Salvador Nicolas
        email = snicoper@gmail.com
    [color]
        ui = true
    [core]
        editor = vim
        autocrlf = input
	    eol = lf
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
    [mergetool "meld"]
        path = "C:\\Program Files (x86)\\Meld\\Meld.exe"
        prompt = false
        keepBackup = false
        trustExitCode = false
        keepTemporaries = false
    [push]
        default = simple

VSCode
======

.. code-block:: bash

    [user]
        name = Salvador Nicolas
        email = snicoper@gmail.com
    [color]
        ui = true
    [core]
        editor = vim
        autocrlf = input
        eol = lf
    [alias]
        lg = log --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr %an)%Creset' --abbrev-commit --date=relative
        co = checkout
        cm = commit
        st = status
        br = branch
    [difftool]
        prompt = false
    [push]
        default = simple
    [diff]
        tool = vscode
    [difftool "vscode"]
        cmd = code --wait --diff $LOCAL $REMOTE
