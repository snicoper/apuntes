.. _reference-git-anadir_en_gitignore_excepto_algun_archivo:

##############################################################################
Añadir a gitignore algunos archivos y quitar otros dentro del mismo directorio
##############################################################################

Si se ha añadido a gitignore un directorio, pero si se quiere tackear algun archivo en especifico
es posible hacerlo con ``!``.

Un ejemplo, se quiere tener control sobre ``media/profiles/avatar.png``, pero
en gitignore media esta añadido.

.. code-block:: bash

    # Añade todo el contenido de media
    media/*

    # Excepto profiles
    !media/profiles

    # Añadir todo el contenido de profiles
    media/profiles/*

    # Excepto la imagen que queremos tener control.
    !media/profiles/avatar.png


