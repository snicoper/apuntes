.. _reference-programacion-uml-relaciones_composicion_agregacion:

###############################
Relación composición agregación
###############################

Fuentes
*******

* http://arodm.blogspot.com/2008/09/uml-relaciones-compocicion-agregacion.html

--------------------

.. note::
    Para ver los diagramas, pinchar en **Fuentes**

Trabajando con los miembros de mi team de desarrollo me di cuenta que a los
programadores le costaba interpretar los Diagramas de Clases que el analista
realizaba. O existían interpretaciones ambiguas de lo que el realizaba,
perdiendo asi la principal funcionalidad del lenguaje UML. Especialmente
en cuanto a las relaciones que existían entre las clases. Por eso me dispuse
a realizar este pequeño documento, donde voy a tratar de explicar que significa
cada relación, en mis palabras, y como se traduce esto a código.

Asociación
**********

.. image:: /_static/uml_asociacion.png

Es generalmente, una relación estructural entre clases, es decir, que en
el ejemplo, existe un atributo de la clase medio de transportes, que es
del tipo Conductor. La navegabilidad nos muestra donde esta ubicado el
atributo. Es decir cual es la clase que tiene contiene el atributo si
ésta no lo mostrase.

Agregación
**********

.. image:: /_static/uml_agregacion.png

Es una relación que se derivó de la asociación, por ser igualmente
estructural, es decir que contiene un atributo, que en todos los
casos, será una colección, es decir un array, vector, etc, y además
de ello la clase que contiene la colección debe tener un método que
agregue los elementos a la colección. También se puede leer como que
un medio de transporte tiene varias ruedas.

Nos esta diciendo que los objetos rueda forman parte del objeto medio
de transporte. Pero, su ciclo de vida no esta atado al del objeto medio
de transporte. Es decir si el automóvil se destruye las ruedas pueden
seguir existiendo independientemente.

Composición
***********

.. image:: /_static/uml_composicion.png

Al igual que en la agregación, es una relación estructural pero se le
suma, que tiene un método de destrucción de los objetos. Y a diferencia
de la asociación, el ciclo de vida del objeto area está relacionado
con el del objeto ruta. Es decir que si la ruta de viaje se levanta,
las áreas que surgían a partir de ella desaparecen. También se puede
leer como que una ruta tiene varias áreas de cobertura.

Mucho se ha discutido a cerca de las agregaciones y las composiciones,
el debate es casi tan caliente como el de los include y extends de los
casos de uso. Ya que algunos sostienen que los lenguajes orientados a
objetos, tienen garbage collector, por lo que no necesitan métodos de
destrucción de los objetos (relacionados a los ciclos de vida en la
composición). Y que la programación es la misma para las composiciones
y las agregaciones, y que la diferencia es meramente conceptual entre
una y otras. Es mas existen varias interpretaciones, pero la expuesta
es la cual yo me adhiero.

Clase de Asociación
*******************

Es una Clase que surge de una multiplicidad de muchos a muchos, y fue
incorporada en UML para dar soporte a este caso. Se sacan los atributos
de las clases involucradas y se los incorpora a una clase a parte.
Al igual que las anteriores hace referencia a una relación estructural.
En el ejemplo son los objetos viaje y ruta.

Realización
***********

Es una relación de contrato con otra clase. Se la utiliza para
implementar una interfaz. En lenguajes como java o php utilizamos
la palabra reservada ``implements``

.. code-block:: console

    public class Viaje implements InterfaceA{…}

Generalmente cuando no estamos seguros si ``algo`` es una interfaz o una
clase abstracta, por que dibujaron los tag que hacen referencias a las
interfaces, debemos ver la relación para saber.

Generalización
**************

Es una relación de herencia. Se puede decir que es un relación
``es un tipo de``. En nuestro ejemplo: “un auto es un tipo de Medio
de transporte”. Es entre una clase hija y su clase madre. En la
codificación podemos encontrar la palabra “extends” que hace referencia
a esta relación. Además podemos encontrar palabras claves tales como
``this`` y ``super`` o ``self`` y ``parent``. Para darnos cuenta que existe
una relación de este tipo involucrada.

.. code-block:: console

    public class Auto extends MedioDeTransporte{…}

Dependencia
***********

Es una relación de uso, es decir que una clase utiliza a otra. Y si esta
ultima se altera, la anterior se puede ver afectada.

En código se suelen traducir principalmente como las clases donde se hace
la instanciación de un objeto. En nuestro ejemplo la clase viaje realiza
los ``new`` de los distintos objetos. En este momento puede que te preguntes
como puede hacer un new de una clase abstracta, jeje. No realiza los new
de la clase abstracta, si no de sus hijas. Seria algo así como

.. code-block:: java

    MedioDeTransporte medio = new Auto();

También se sostiene que este tipo de relación hace referencias, a los
parámetros que se pasan en un método, bajo este concepto, en java,
podría ser algo así como:

.. code-block:: java

    public void crearViaje(MedioDeTransporte medio) {}

Por ultimo también se sostiene que podemos codificar esta relación
realizando un ``return`` del tipo de dato en algún método.

Bueno espero haber limpiado algunas dudas, hay mucho para discutir
sobre el asunto.
