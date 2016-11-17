.. _reference-editors-vim-vim_spf13:

#########
Vim spf13
#########

`GitHub spf13 <https://github.com/spf13/spf13-vim>`_

Para el corrector en español, :ref:`reference-editors-vim-spell_vim_es`

.. code-block:: bash

    vim ~/.vimrc.local

.. code-block:: bash

    " { Basicas

        set mouse=
        set nofoldenable
        let g:indent_guides_enable_on_vim_startup = 0

    " }

    " { Syntastic

        let g:syntastic_check_on_open = 1
        let g:syntastic_python_flake8_post_args='--ignore=E501,D100,D101,D102,D105,W391'

    " }

    " { Corector español

        set spell
        setlocal spell spelllang=es
        set spellfile=~/.vim/dict_es.add

    " }

.. code-block:: bash

    vim ~/.vimrc.bundles.local

.. code-block:: bash

    Plugin 'editorconfig/editorconfig-vim'
    Plugin 'jszakmeister/vim-togglecursor'
    "Plugin 'mjbrownie/django_completeme'

PYTHONPATH
==========

.. code-block:: bash

    vim ~/.bashrc

    # Añadir
    export PYTHONPATH="${PYTHONPATH}:/home/snicoper/.virtualenvs/default/lib/python3.5/site-packages"

