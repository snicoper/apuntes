.. _reference-editors-vim-spell_vim_es:


##########################
Poner Vim spell en español
##########################

**Fuentes**

* http://plagatux.es/2008/12/correcion-ortografica-en-vim/

-----

Descargar de `aquí <http://ftp.vim.org/vim/runtime/spell/>`_ los archivos:

* es.latin1.spl
* es.latin1.sug
* es.utf-8.spl
* es.utf-8.sug

Imaginando que los archivos están en `~/Downloads/spell/` hay que copiarlos a `/usr/share/vim/vim74/spell`

.. code-block:: bash

    cd ~/Downloads/spell/
    sudo cp ./* /usr/share/vim/vim74/spell/


Ahora editamos el `vimrc`

.. code-block:: bash

    vim ~/.vimrc

    # Añadimos
    set spell
    setlocal spell spelllang=es

Si queremos añadir palabras a nuestro diccionario, en `vimrc` añadir.

.. code-block:: bash

    set spellfile=~/.vim/dict_es.add

* ]s – Siguiente falta ortográfica
* [s – Anterior falta ortográfica
* z= – Mostrar sugerencias para una palabra incorrecta.
* zg – Añadir una palabra al diccionario.
* zug – Deshacer la adición de una palabra al diccionario.
* zw – Eliminar una palabra del diccionario.
