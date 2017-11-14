.. _reference-linux-montar_imagenes_bin_iso_etc:

####################################
Mostrar Imagenes BIN, ISO, CUE, etc.
####################################

Fuente:
*******

* http://bronch.wordpress.com/2006/05/24/como-montar-archivos-iso-bin-mdf-y-nrg-en-linux/

.. note::
    [ Créditos: este “howto” está basado en parte en las instrucciones que da Rodrigo
    Perez en este post aunque no he incluido algunos de sus métodos porque no los he probado
    personalmente. Además se ha utilizado información encontrada en los foros de
    Ubuntu-es.org así como en la Guia-Ubuntu -versión Breezy-. Para los archivos IMG
    se ha usado la información encontrada en este foro. Las instrucciones para
    convertir imágenes DAA las encontré en esta guía que además incluye otras
    instrucciones para manipular archivos DAA.)

Linux tiene la posibilidad de montar las imágenes de cd/dvd sin tener que grabarlas.
Asumiremos que usas una distribución que usa “apt” para instalar y actualizar
paquetes, este es el caso de debian, ubuntu, suse,etc. Asumiremos también que sabes
como crear directorios y que sabes qué es “montar” un sistema de ficheros.
Vamos al grano.

Con unos cuantos comandos de consola podremos montar distintos tipos de imágenes
de CD/DVD fácilmente:

Lo más básico, montar una imagen ISO:
*************************************

.. code-block:: bash

    sudo mount -t iso9660 -o loop archivo.iso /directorio/de/montaje

Montando imágenes BIN y CUE:
****************************

Para poder montar estos archivos necesitas convertirlos antes a imagen ISO, esto
lo puedes hacer con el programa bchunk.

(Si no tienes instalado bchunk)

.. code-block:: bash

    sudo apt-get install bchunk

.. note::
    si así no puedes instalarlo puede encontrar el programa
    `aqui <http://he.fi/bchunk/>`_ : bchunk

y cuando se haya instalado procederemos a convertir la imagen bin con su archivo
cue correspondiente a un solo archivo iso:

.. code-block:: bash

    bchunk archivo.bin archivo.cue nuevonombre.iso

Ahora ya tendrás un nuevo archivo iso que podrás montar como se explica más arriba.

Montar imágenes NRG (imágenes de Nero Burning Rom):
***************************************************

Las imágenes NRG pueden ser montadas directamente sin necesidad de convertirlas:

.. code-block:: bash

    mount -t iso9660 -o loop,offset=307200 imagen.nrg /directorio/de/montaje

Si tienes algún problema con ese método o deseas convertir la imagen NRG a ISO
deberás usar el programa nrg2iso, para instalarlo haremos:

.. code-block:: bash

    sudo apt-get install nrg2iso


si así no puedes instalarlo puede encontrar el programa aquí:
`Nrg2Iso <http://gregory.kokanosky.free.fr/v4/linux/nrg2iso.en.html>`_
y cuando ya esté instalado, para convertir la imagen

.. code-block:: bash

    nrg2iso archivo.nrg nuevoarchivo.iso

y para montar la imagen ISO simplemente debes seguir las instrucciones detalladas
más arriba

Montar imágenes MDF y MDS
*************************

De nuevo utilizaremos un programa para convertir antes la imagen mdf a iso. El
programa tiene el original nombre de mdf2iso. Para instalarlo:

.. code-block:: bash

    sudo apt-get install mdf2iso

si así no puedes instalarlo puede encontrar el programa aquí:
`Mdf2Iso <http://developer.berlios.de/projects/mdf2iso>`_)
y una vez instalado convertiremos el archivo MDF a ISO

.. code-block:: bash

    mdf2iso archivo.mdf nuevaimagen.iso

Montar imágenes IMG
*******************

Usaremos el programa CCD2ISO. Este programa no lo he podido descargar desde los
repositorios oficiales de Ubuntu pero de todos modos no estaría de más que
intentases instalarlo por apt-get así:

.. code-block:: bash

    sudo apt-get install ccd2iso

Si de este modo no puedes instalarlo puedes seguir las instrucciones de
esta página para bajar el paquete deb de
`ccd2iso <http://www.ubuntu-es.org/index.php?q=node/31266>`_
e instalarlo fácilmente.

Si por cualquier motivo no pudieses conseguir el programa por esos dos métodos
siempre puedes descargarlo desde su página:
`ir a Ccd2Iso <http://sourceforge.net/projects/ccd2iso>`_ (ojo, tendrás que compilarlo)

Para instalarlo de este último modo descargamos el archivo que sera algo así
como “ccd2iso-0.2.tar.gz” (puede variar la versión) y primero lo descomprimimos así:

.. code-block:: bash

    tar -xzvf ccd2iso-0.2.tar.gz

Ahora que tendremos un directorio llamada “ccd2iso”, hacemos lo siguiente:

.. code-block:: bash

    cd ccd2iso

    ./configure

    make
    make install

Con esto ya tendremos instalado el programa ccd2iso. Finalmente para convertir
la imagen ccd a iso hacemos:

.. code-block:: bash

    ccd2iso imagen.img imagen.iso

Y montaremos la imagen iso recien creada como se explica más arriba en esta
misma guía.

Montar imágenes DAA
*******************

El formato DAA es un formato que utiliza el programa Poweriso. Durante algún
tiempo este formato resultaba muy difícil de utilizar en Linux (no había versión
de Poweriso para linux y la emulación con wine no funcionaba). Finalmente los
creadores del programa sacaron una versión gratuita de su programa para Linux que
además nos sirve para convertir otros formatos.

Pero vamos al grano, para convertir una imagen DAA a ISO primero necesitaremos
la `versión linux de poweriso que podemos bajar desde esta página <http://poweriso.com/download.htm>`_
(parte de abajo) o bien de esta forma :

.. code-block:: bash

    wget http://poweriso.com/poweriso.tar.gz

Descomprimimos

.. code-block:: bash

    tar -zxvf poweriso.tar.gz

Y convertimos a ISO:

.. code-block:: bash

    ./poweriso convert imagen.daa -o nuevaimagen.iso

(Instrucciones para montar la imagen iso, al principio de esta guía)
