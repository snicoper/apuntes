.. _reference-editors-vscode-configuracion:

##################
Visual Studio Code
##################

Algunos tips

Task Runner
===========

``Ctrl+Mayus+P`` **->** ``Tasks: Configure Task Runner -> Other``

.. code-block:: bash

    {
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
        "version": "0.1.0",
        "command": "/home/snicoper/.virtualenvs/default/bin/python",
        "isShellCommand": true,
        "args": ["${file}"],
        "showOutput": "always"
    }

``Ctrl+Mayus+B`` para ejecutar archivo.
