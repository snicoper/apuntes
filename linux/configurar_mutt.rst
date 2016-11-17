.. _reference-linux-configurar_mutt:

###############
Configurar mutt
###############

**Fuentes**

* http://www.elho.net/mutt/maildir/

----

.. code-block:: bash

    # Fedora
    vim /etc/Muttrc

.. code-block:: bash

    # Linea 1108
    set folder="~/Maildir"

    # Linea 2074
    set mask="!^\\.[^.]"

    # Linea 2086
    set mbox="~/Maildir"

    # Linea 2099
    set mbox_type=Maildir

    # Linea 3130
    set postponed="+.Drafts"

    # Linea 3395
    set record="+.Sent"

    # Linea 4378
    set spoolfile="~/Maildir"

Para entrar al correo, simplemente ``mutt``

