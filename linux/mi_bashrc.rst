.. _reference-linux-mi_bashrc:

##########
Mi .bashrc
##########

**Fuentes**

* https://github.com/magicmonty/bash-git-prompt

----

bash-git-prompt
===============

.. code-block:: bash

    cd ~
    git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1

.. code-block:: bash

    vim ~/.bashrc

    GIT_PROMPT_ONLY_IN_REPO=0
    source ~/.bash-git-prompt/gitprompt.sh
