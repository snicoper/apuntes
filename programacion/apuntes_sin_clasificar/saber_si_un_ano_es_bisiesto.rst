.. _reference-programacion-apuntes_sin_clasificar-saber_si_un_ano_es_bisiesto:

###########################
Saber si un año es bisiesto
###########################

.. code-block:: php

    if ((($year % 4 == 0) && ($year % 100 != 0)) || ($year % 400 == 0)) {
        $bisiesto = true;
    }
