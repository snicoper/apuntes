.. _reference-programacion-pcre-verificacion_email_pcre:

##############################
Verificación de Email con PCRE
##############################

PHP
***

.. code-block:: php

    <?php

    $pattern = '/^([a-z0-9])(([-a-z0-9._])*([a-z0-9]))*\@([a-z0-9])'
        . '(([a-z0-9-])*([a-z0-9]))+(\.([a-z0-9])([-a-z0-9_-])?([a-z0-9])+)+$/i';

Python
******

.. code-block:: python

    pattern = '{0}{1}'.format(
        r'^([a-z0-9])(([-a-z0-9._])*([a-z0-9]))*@([a-z0-9])',
        r'(([a-z0-9-])*([a-z0-9]))+(.([a-z0-9])([-a-z0-9_-])?([a-z0-9])+)+$')

Javascript
**********

.. warning::
    POR HACER

C#
***

.. code-block:: c#

    using System.Text.RegularExpressions;

    string pattern = @"^([a-z0-9])(([-a-z0-9._])*([a-z0-9]))*\@([a-z0-9])" +
        @"(([a-z0-9-])*([a-z0-9]))+(\.([a-z0-9])([-a-z0-9_-])?([a-z0-9])+)+$";

    Regex regex = new Regex(pattern, RegexOptions.IgnoreCase);
    bool isValid = regex.IsMatch("snicoper@example.com");

HTML5
*****

.. warning::
    No probada

.. code-block:: html

    ^([a-z0-9])(([-a-z0-9._])*([a-z0-9]))*\@([a-z0-9])(([a-z0-9-])*([a-z0-9]))+(\.([a-z0-9])([-a-z0-9_-])?([a-z0-9])+)+$'
