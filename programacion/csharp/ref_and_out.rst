.. _reference-programacion-csharp-ref_and_out:

###########
ref and out
###########

Sirven para usar variables como referencias en los métodos.

Tanto ref, como out, no se pueden usar en parámetros opcionales.

Reglas de ref
*************

* El parámetro pasado al método, ha de estar declarado e inicializado
* El método se le ha de añadir 'ref' (ref int i)
* Al llamar el método, en el parámetro se ha de volver a usar 'ref' LlamarMethod(ref i)

Reglas de out
*************

* El argumento dentro del método (referencia a), se le ha de dar un valor antes de que termine el método.
* Tanto el parámetro como el argumento, es necesario indicarlo con 'out tipo nombre'
