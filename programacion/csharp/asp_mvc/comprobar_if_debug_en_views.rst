.. _reference-programacion-asp_mvc-comprobar_if_debug_en_views:

##########################
Comprobar if debug en View
##########################

**Fuentes**

* https://stackoverflow.com/a/15359611

------------------------

.. code-block:: csharp

    @if (HttpContext.Current.IsDebuggingEnabled)
    {
        // Means that debug="true" in Web.config
    }