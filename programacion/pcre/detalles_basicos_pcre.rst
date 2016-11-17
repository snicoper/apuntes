.. _reference-programacion-pcre-detalles_basicos_pcre:

########################
Detalles basicos en PCRE
########################

Fuentes
*******

* http://es.php.net/manual/es/book.pcre.php
* http://www.php.net/manual/es/regexp.reference.meta.php
* http://www.php.net/manual/es/regexp.reference.escape.php#regexp.reference.escape

---------------

Meta-caracteres
***************

* (*) 0 o mas instancias de dicha expresión regular
* (|) Expresión regular compuesta por la expresión regular izquierda o derecha
* (^) Para identificar el inicio de una cadena
* ([^a-z]) Sirve para decir que no puede contener la expresión, en este caso cualquier letra en minúsculas.
* ($) Para identificar el final de una cadena
* (.) Para identificar la expresión "cualquier carácter"
* (+) Expresión regular compuesta por una o mas instancias de dicha expresión regular
* (?) Expresión regular compuesta por 0 o 1 instancia de dicha expresión regular
* ({max,min}) Expresión regular compuesta por un numero de variable de instancias de dicha Expresión Regular. El parámetro min indica el mínimo de numero de instancias aceptables, mientras que el parámetro max, si lo hubiera, indica el máximo numero de instancias aceptables. Si solo se encuentra min y la coma disponible, no existe ningún limite superior en cuanto al numero de instancias que podemos encontrar en la cadena. Por ultimo si solo definimos min sin la coma significara el único numero de instancias aceptable.
* ([]) Sirve para identificar grupos de caracteres aceptables para una determinada posición.

Secuencias de escape
********************

* (\w) Representa un carácter de "palabra" y es equivalente a la expresión [a-zA-Z0-9\_]
* (\W) Representa lo opuesto a \w y es equivalente a [^a-zA-Z0-9\_]
* (\s) Representa un carácter de espacio en blanco
* (\S) Representa un carácter que no es un espacio en blanco
* (\d) Representa un dígito, equivalente a [0-9]
* (\D) Representa un carácter que no es un dígito, equivalente a [^0-9]
* (\n) Representa un carácter de nueva linea
* (\r) Representa un carácter de retorno de carro
* (\t) Representa un carácter de tabulación
