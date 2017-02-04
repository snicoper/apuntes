.. _reference-editors-atom-spell_check_spanish.rst:

########################
Atom Spell Check Spanish
########################

Lo primero que probe con ``hunspell``, pero la codificación de caracteres me daba error
en los acentos y las eñes me salia el típico ``�``.

https://github.com/atom/spell-check/issues/161

De todas formas dejo el apunte para un futuro, aunque yo uso la `Opción 2`_.

Opción 1
********

Supongo que esto es valido para cualquier linux y ¿osx?, yo lo hago en fedora.

Tener instalados los diccionarios del idioma, en mi caso ``hunspell-es``.

.. code-block:: bash

    sudo dnf install -y hunspell-es

Averiguar el directorio de los diccionarios (no he encontrado una mejor manera para averiguar el directorio)

.. code-block:: bash

    hunspell -D
    # Ctrl+C para salir

En mi caso todos empiezan por ``/usr/share/myspell/xx_XX``

En Atom, ``Settings -> Packages`` buscar ``spell-check``

**Grammars**

En **Grammars** poner los **languages** donde usar ``spell-check``, para saber un grammar
abrir el archivo y pulsar ``Ctrl+Shift+P`` e introducir ``Editor: Log Cursor Scope``.
Copiar lo que muestre y pegarlo en **Grammars**.

**Locale Paths**

Añadir ``/usr/share/myspell``

**Locales**

.. code-block:: bash

    ls /usr/share/myspell

Añadir el/los diccionarios que se quieran, se puede tener ingles y español a la vez, separados
por comas (omitir la extension ``.dic .aff``)

En mi caso: ``en_US, es_ES``

Opción 2
********

Esta opción también es valida para Windows modificando las rutas.

.. code-block:: bash

    # Crear directorio para descargar los diccionarios.
    mkdir ~/sources

    cd ~/sources
    git clone git://github.com/titoBouzout/Dictionaries.git Dictionaries

**Grammars**

Igual que la `Opción 1`_

**Locale Paths**

Añadir ``/home/TU_USER/sources/Dictionaries``, Cambiar la ruta por una correcta.

**Locales**

.. code-block:: bash

    Spanish, English (American)

El nombre de uno de los archivos en ``/home/TU_USER/sources/Dictionaries``, sin la extensión.

keymaps
*******

``Edit -> Keymap...``

.. code-block:: console

    'atom-text-editor':
        'alt-d': 'spell-check:toggle'
        'alt-s': 'spell-check:correct-misspelling'

El primero para activar/desactivar, el segundo para mostrar sugerencias de corrección cuando esta
el cursor encima de la palabra.

Final
*****

Por defecto al abrir un archivo, esta activo el corrector, algo que molesta sobre todo
cuando estas con lenguajes de programación y has estar dando siempre ``Ctrl+D`` para verlo
con menos ruido.

Para que este desactivado al abrir un archivo, editar ``Edit -> Init Script...`` y añadir:

.. code-block:: console

    # Por defecto, spell-check disable al abrir
    atom.workspace.observeTextEditors (editor) ->
      setTimeout ->
        atom.commands.dispatch atom.views.getView(editor), 'spell-check:toggle'
      , 0 if editor.editorElement.spellcheck
