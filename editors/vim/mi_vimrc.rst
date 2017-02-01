.. _reference-editors-vim-mi_vimrc:

#########
Mi .vimrc
#########

Opción 1
========

.. code-block:: bash

    vim ~/.vimrc

.. code-block:: vim

    set pastetoggle=<F2>
    set clipboard=unnamed
    set encoding=utf8

    " Rebind <Leader> key
    let mapleader = ","

    " Enable syntax highlighting
    " You need to reload this file for the change to apply
    filetype off
    filetype plugin indent on
    syntax on
    set scrolloff=8

    " Showing line length
    set nonu
    set tw=79   " width of document (used by gd)
    set nowrap  " don't automatically wrap on load
    set fo-=t   " don't automatically wrap text when typing
    set colorcolumn=100
    highlight ColorColumn ctermbg=233

    " Useful settings
    set history=700
    set undolevels=700

    " Real programmers don't use TABs but spaces
    autocmd Filetype python setlocal expandtab tabstop=4 shiftwidth=4
    autocmd Filetype md setlocal expandtab tabstop=4 shiftwidth=4
    autocmd Filetype rst setlocal expandtab tabstop=4 shiftwidth=4
    set tabstop=2
    set softtabstop=2
    set shiftwidth=2
    set shiftround
    set expandtab

    " Make search case insensitive
    set hlsearch
    set incsearch
    set ignorecase
    set smartcase

    " Disable stupid backup and swap files - they trigger too many events
    " for file system watchers
    set nobackup
    set nowritebackup
    set noswapfile

    " Split navigations
    nnoremap <C-J> <C-W><C-J>
    nnoremap <C-K> <C-W><C-K>
    nnoremap <C-L> <C-W><C-L>
    nnoremap <C-H> <C-W><C-H>

    " Stupid shift key fixes
    command! -bang -nargs=* -complete=file E e<bang> <args>
    command! -bang -nargs=* -complete=file W w<bang> <args>
    command! -bang -nargs=* -complete=file Wq wq<bang> <args>
    command! -bang -nargs=* -complete=file WQ wq<bang> <args>
    command! -bang Wa wa<bang>
    command! -bang WA wa<bang>
    command! -bang Q q<bang>
    command! -bang QA qa<bang>
    command! -bang Qa qa<bang>

Opción 2
========

.. code-block:: bash

    vim ~/.vimrc

.. code-block:: bash

    set pastetoggle=<F2>
    set clipboard=unnamed
    set encoding=utf8

    " Rebind <Leader> key
    let mapleader = ","

    " Enable syntax highlighting
    " You need to reload this file for the change to apply
    filetype off
    filetype plugin indent on
    syntax on
    set scrolloff=8

    " Showing line length
    set nonu
    set tw=79   " width of document (used by gd)
    set nowrap  " don't automatically wrap on load
    set fo-=t   " don't automatically wrap text when typing
    set colorcolumn=100
    highlight ColorColumn ctermbg=233

    " color
    let g:molokai_original = 1
    colo molokai

    " Useful settings
    set history=700
    "set undolevels=700
    set foldlevel=99

    " Real programmers don't use TABs but spaces
    set tabstop=4
    set softtabstop=4
    set shiftwidth=4
    set shiftround
    set expandtab

    " Make search case insensitive
    set hlsearch
    set incsearch
    set ignorecase
    set smartcase

    " Disable stupid backup and swap files - they trigger too many events
    " for file system watchers
    set nobackup
    set nowritebackup
    set noswapfile

    " Split navigations
    nnoremap <C-J> <C-W><C-J>
    nnoremap <C-K> <C-W><C-K>
    nnoremap <C-L> <C-W><C-L>
    nnoremap <C-H> <C-W><C-H>

    " Stupid shift key fixes
    command! -bang -nargs=* -complete=file E e<bang> <args>
    command! -bang -nargs=* -complete=file W w<bang> <args>
    command! -bang -nargs=* -complete=file Wq wq<bang> <args>
    command! -bang -nargs=* -complete=file WQ wq<bang> <args>
    command! -bang Wa wa<bang>
    command! -bang WA wa<bang>
    command! -bang Q q<bang>
    command! -bang QA qa<bang>
    command! -bang Qa qa<bang>

    " Tabs, buffers
    map <C-n> :bprev<Return>
    map <C-m> :bnext<Return>
    map <C-right> :tabn <Return>
    map <C-left> :tabp <Return>

    " Plug
    call plug#begin('~/.vim/plugged')

    Plug 'scrooloose/nerdtree'
    Plug 'jistr/vim-nerdtree-tabs'
    Plug 'Xuyuanp/nerdtree-git-plugin'
    Plug 'klen/python-mode'
    Plug 'editorconfig/editorconfig-vim'
    Plug 'ctrlpvim/ctrlp.vim'
    Plug 'vim-airline/vim-airline'
    Plug 'tpope/vim-fugitive'
    Plug 'airblade/vim-gitgutter'
    Plug 'alvan/vim-closetag'
    Plug 'jiangmiao/auto-pairs'
    Plug 'tomasr/molokai'
    Plug 'Valloric/YouCompleteMe'
    Plug 'SirVer/ultisnips'
    Plug 'honza/vim-snippets'

    call plug#end()

    " nerdtree
    map <F5> :NERDTreeToggle<CR>
    "let g:nerdtree_tabs_open_on_console_startup = 1

    " airline
    set laststatus=2
    let g:airline#extensions#tabline#enabled = 1

    " YouCompleteMe
    let g:ycm_python_binary_path = '/home/snicoper/.virtualenvs/default/bin/python'
    let g:ycm_collect_identifiers_from_tags_files = 1 " Let YCM read tags from Ctags file
    let g:ycm_use_ultisnips_completer = 1 " Default 1, just ensure
    let g:ycm_seed_identifiers_with_syntax = 1 " Completion for programming language's keyword
    let g:ycm_complete_in_comments = 1 " Completion in comments
    let g:ycm_complete_in_strings = 1 " Completion in string

    " ultisnips
    let g:UltiSnipsExpandTrigger = '<C-j>'
    let g:UltiSnipsJumpForwardTrigger = '<C-j>'
    let g:UltiSnipsJumpBackwardTrigger = '<C-k>'

.. code-block:: bash

    vim

    :PlugInstall

.. code-block:: bash

    sudo dnf install automake gcc gcc-c++ kernel-devel cmake python3-devel

    cd ~/.vim/plugged/YouCompleteMe
    ./install.sh --clang-completer --system-libclang

.. code-block:: bash

    mkdir -p ~/.vim/colors
    ln -s ~/.vim/plugged/molokai/colors/molokai.vim ~/.vim/colors/molokai.vim
