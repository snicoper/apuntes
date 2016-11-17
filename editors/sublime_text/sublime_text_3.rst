.. _reference-editors-sublime_text-sublime-text-3:

##############
Sublime Text 3
##############

..warning

    DEPRECATED, ya no lo uso y dejo de actualizarlo.

Instalacion de Package Control
******************************

``Ctrl+Shift+P``: ``Install Package Control``

Packages
********

* DocBlockr
* EditorConfig
* Color Highlighter
* Plain​Tasks

Git
***

* GitGutter
* Git
* SideBarGit

Sass
****

* SCSS

Python
******

* Anaconda
* Djaneiro

React.js
********

* Babel (no)
* ReactJS (no)

Theme
*****

* OneDark Material

Linters
*******

* SublimeLinter
* SublimeLinter-rst
* SublimeLinter-json

Buscar los nuevos

Configuracion
*************

Esta configuración la uso tanto en Linux como en Windows, solo mirar que
la fuente este instalada o cambiar por otra, también ajustar tamaño fuente.

El ```"theme"``` y/o el ```"color_scheme"```, pueden variar también.

Abrir Preferences > Setting - User

.. code-block:: javascript

    {
        // Colors and theme
        "color_scheme": "Packages/User/SublimeLinter/OneDark (SL).tmTheme",
        "theme": "OneDarkMaterial.sublime-theme",

        // Theme Material Theme
        "material_theme_accent_purple" : true ,
        "always_show_minimap_viewport" : true,
        "bold_folder_labels"           : true,
        "font_options"                 : [ "gray_antialias", "subpixel_antialias" ],    // On retina Mac & Windows
        "indent_guide_options"         : [ "draw_normal", "draw_active" ],   // Highlight active indent
        "line_padding_bottom"          : 3,
        "line_padding_top"             : 3,
        "overlay_scroll_bars"          : "enabled",

        // Font
        "font_face": "DejaVu Sans Mono",

        // Editor view look-and-feel
        "highlight_line": true,
        "show_minimap": false,
        "caret_extra_width": 2,
        "show_encoding": true,
        "show_line_endings": true,
        "bold_folder_labels": true,

        // Editor behavior
        "highlight_modified_tabs": true,
        "find_selected_text": true,
        "shift_tab_unindent" : false,
        "tab_completion": false,
        "vintage_start_in_command_mode": true,

        // Word wrapping - follow PEP 8 recommendations
        "rulers": [ 100 ],
        "word_wrap": false,

        // Whitespace - no tabs, trimming, end files with \n
        "tab_size": 4,
        "translate_tabs_to_spaces": true,
        "trim_trailing_white_space_on_save": true,
        "ensure_newline_at_eof_on_save": true,

        // Sidebar - exclude distracting files and folders
        "file_exclude_patterns":
        [
            ".DS_Store",
            "*.pyc",
            ".directory"
        ],
        "folder_exclude_patterns":
        [
            ".git",
            ".svn",
            ".hg",
            "__pycache__",
            ".idea"
        ],
        "ignored_packages":
        [
        ]
    }

Key bindings
************

Algunas combinaciones de teclas no me funciona por defecto, por lo que
tengo configuradas una pocas.

Algunas sin modificar si funcionan en Windows, pero para no tener 2
diferentes, uso esta configuración en ambos sistemas.

.. code-block:: javascript

    [
        // Indetntar codigo
        { "keys": ["alt+."], "command": "indent" },

        // DesIndentar codigo
        { "keys": ["alt+,"], "command": "unindent" },

        // Comentar linea
        { "keys": ["alt+c"], "command": "toggle_comment", "args": { "block": false } },

        // Comentar bloque
        { "keys": ["alt+b"], "command": "toggle_comment", "args": { "block": true } },

        // Join lines
        { "keys": ["ctrl+j"], "command": "join_lines" },

        // Markdown preview
        { "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },

        // Word wrap
        { "keys": ["alt+w"], "command": "toggle_setting", "args": {"setting": "word_wrap"} },

        // Reformat code
        { "keys": ["alt+r"], "command": "reindent" , "args": { "single_line": false } }
    ]

SublimeLinter
*************

``Preferences -> Package Settings -> SublimeLinter -> Settings - User``

**NOTA:** Si el archivo esta vacío, ``Ctrl+S``, cerrar y volver a abrir.

# Añadir dentro de ``"user": {``

.. code-block:: javascript

    "user": {
        "lint_mode": "load/save"
    }

Anaconda
********

**Fuentes**

* https://github.com/DamnWidget/anaconda/blob/master/Anaconda.sublime-settings

----

La configuración se pone en
``Preferences -> Package Settings -> Anaconda -> Settings - User``.

Por defecto tengo un **virtualenv**, para proyectos poner la configuracion a nivel de proyecto
o cambiar el ``python_interpreter``

.. code-block:: javascript

    {
        "python_interpreter": "/home/snicoper/.virtualenvs/default/bin/python",
        "anaconda_linter_mark_style": "none",
        "complete_parameters": false,
        "anaconda_gutter_theme": "alpha",
        "display_signatures": true,
        "pep8_max_line_length": 100,
        "auto_formatting": false,
        "pep8_ignore":
        [
        ],
    }

Poner diccionario castellano
****************************

**Fuentes**

* http://www.snicoper.com/blog/article/poner-diccionario-espanol-en-sublime-text-3/

----

Linux
^^^^^

.. code-block:: bash

    cd ~/Downloads
    git clone git://github.com/SublimeText/Dictionaries.git Dictionaries

    mkdir -p ~/.config/sublime-text-3/Packages/Language

    cp Dictionaries/Spanish.* ~/.config/sublime-text-3/Packages/Language

En ``ST``, en el menú ``View -> Dictionary``, seleccionamos el idioma y luego para resaltar los errores de idioma le damos a ``F6``.

Windows
^^^^^^^

Todo igual que en Linux, pero el directorio ``Language`` se crea en ``~\AppData\Roaming\Sublime Text 3\Packages``, dentro poner archivos ``Dictionaries/Spanish.*``.
