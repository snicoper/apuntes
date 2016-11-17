.. _reference-editors-atom-configuracion:

##################
Configuración Atom
##################

Algunos tips

Spell-Check español
*******************

Primero hacer un backup, de los diccionarios que vienen por defecto (ingles).

.. code-block:: bash

    cd /usr/share/atom/resources/app.asar.unpacked/node_modules/spell-check/node_modules/spellchecker/vendor/hunspell_dictionaries

    sudo cp en_US.aff en_US.aff.back
    sudo cp en_US.dic en_US.dic.back

Descargar diccionarios desde GitHub y moverlos.

.. code-block:: bash

    cd ~/Downloads
    git clone git://github.com/SublimeText/Dictionaries.git Dictionaries
    cd Dictionaries

    sudo cp Spanish.aff /usr/share/atom/resources/app.asar.unpacked/node_modules/spell-check/node_modules/spellchecker/vendor/hunspell_dictionaries/en_US.aff
    sudo cp Spanish.dic /usr/share/atom/resources/app.asar.unpacked/node_modules/spell-check/node_modules/spellchecker/vendor/hunspell_dictionaries/en_US.dic

``Edit -> Preferences -> Packages -> Spell Check``

En ``Grammars`` añadir la lista de lenguajes. Para conocer el **grammar** de un lenguaje pulsar ``Ctrl+Shift+Alt+P`` o ``Ctrl+Shift+P`` y escribir ``Editor: Log Cursor Scope``.
