.. _reference-programacion-csharp-up_down_cast:

#################
Upcast y Downcast
#################

Fuentes
*******

* http://www.programacion.com/foros/java-basico/que_es_downcasting_170402

Queremos guardar una serie de objetos Silla en un ArrayList.

El ArrayList sólo admite objetos de tipo Object, pero como Silla hereda de Object
(como todos los objetos) puedes meter sillas directamente en el ArrayList:

.. code-block:: c#

    ArrayList miLista = new ArrayList();
    miLista.add(new Silla());

Cuando metes un objeto Silla en un ArrayList, Jaa hace un cast implícito al tipo
Object. Esto se conoce como "upcasting", es decir, moldear un objeto al tipo de
una de sus superclases.

Ahora bien, si necesitamos recuperar uno de esos objetos Silla, debemos hacer
lo siguiente:

.. code-block:: c#

    Silla s = (Silla)miLista.get(0);

El cast es necesario porque el método get() devuelve objetos de tipo Object.
Pues bien, a esta operación se le llama "downcasting", porque estás moldeando
un objeto a una de sus subclases.

Ahora cuidado: no puedes moldear un objeto Silla a Object y luego moldear ese
Object a Mesa, por ejemplo, porque no funcionará. Sólo puedes hacer upcasting
y downcasting dentro de la jerarquía de herencia del objeto, o dicho de otra
forma, sólo puedes moldear el objeto a una de las clases comprendidas entre la
clase Object y el tipo original del objeto (ambos inclusive), pasando por todas
sus superclases.
