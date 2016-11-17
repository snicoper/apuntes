.. _reference--windows-instalar_cygwin:

###############
Instalar Cygwin
###############


Fuentes
*******

* http://www.cygwin.com/

-----------

Descargar el instalador e instalar. La primera vez que lo instalo, lo instalo sin
elegir nada, cuando a acabado la primera instalación, lo vuelvo a ejecutar y
selecciono los paquetes a instalar.

.. code-block:: bash

    openssh
    wget
    ca-certificates
    curl
    tree

Añadir al path

.. code-block:: bash

    C:\cygwin64\bin;

Instalar `apt-cyg <https://github.com/transcode-open/apt-cyg>`_

.. code-block:: bash

    wget rawgit.com/transcode-open/apt-cyg/master/apt-cyg
    install apt-cyg /bin

Modificar ``C:\cygwin64\home\snicoper\.bashrc``

.. code-block:: bash

    alias ll='ls -lF'
    alias la='ls -a'
    alias lla='ll -a'
    alias statc='stat -c %a'
    alias ccat='pygmentize -g'

    # Git
    function git_branch {
        git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1) /'
    }

    PS1='\[\e[0;32m\]\u@\[\e[m\]\[\e[0;32m\]\h\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\n\[\033[0;32m\]$(git_branch)\[\033[00m\]\$ '

