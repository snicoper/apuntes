.. _reference-linux-instalar_oh-my-zsh:

##################
Instalar oh-my-zsh
##################

* https://github.com/robbyrussell/oh-my-zsh

.. code-block:: bash

    sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
    git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
    git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt"
    ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"

.. code-block:: bash

    vim ~/.zshrc

    # Cambiar theme
    ZSH_THEME="spaceship"

    # plugins
    plugins=(git zsh-autosuggestions)
