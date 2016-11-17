.. _reference-programacion-csharp-diferencia_class_and_struct:

.. |br| raw:: html

    <br />

###############################
Diferencia entre Class y Struct
###############################

Fuentes
*******

* http://geekswithblogs.net/BlackRabbitCoder/archive/2010/07/29/c-fundamentals-the-differences-between-struct-and-class.aspx

---------

La primera gran diferencia es que las clases son tipo referencia mientras que las structs
son tipo valor.

Algunas diferencias
*******************

.. note::
    En `geekswithblogs.net <http://geekswithblogs.net/BlackRabbitCoder/archive/2010/07/29/c-fundamentals-the-differences-between-struct-and-class.aspx>`_
    hay un articulo mucho mas completo.

+-----------------------------------+------------+------------+------------------------------------------+
| Feature                           | Struct     | Class      | Notes                                    |
+===================================+============+============+==========================================+
| Is a reference type?              | No         | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Is a value type?                  | Yes        | No         |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have nested Types             | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| (enum, class, struct)?            |            |            |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have constants?               | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have fields?                  | Yes        | Yes        | Campos de instancia estructura no se |br||
|                                   |            |            | pueden inicializar, se inicializará  |br||
|                                   |            |            | automáticamente al valor por defecto.    |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have properties?              | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have indexers                 | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have methods                  | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have Events                   | Yes        | Yes        | Las estructuras, al igual que las    |br||
|                                   |            |            | clases, pueden tener eventos, pero   |br||
|                                   |            |            | se debe tener cuidado de que no se   |br||
|                                   |            |            | suscribe a una copia de una          |br||
|                                   |            |            | estructura en lugar de la estructura |br||
|                                   |            |            | que pretende.                            |
+-----------------------------------+------------+------------+------------------------------------------+
| Can have static members           | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| (constructors, fields,        |br|| No         | Yes        | Las clases pueden heredar de otras   |br||
| methods, properties,          |br||            |            | clases (o de objeto por defecto).    |br||
| etc.)? Can inherit?               |            |            | Las estructuras siempre heredan de   |br||
|                                   |            |            | ``System.ValueType`` y se sellan de  |br||
|                                   |            |            | manera implícita                         |
+-----------------------------------+------------+------------+------------------------------------------+
| Can implement interfaces?         | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can overload constructor?         | No         | Yes        | Sobrecarga de estructura del         |br||
|                                   |            |            | constructor no oculta constructor    |br||
|                                   |            |            | predeterminado                           |
+-----------------------------------+------------+------------+------------------------------------------+
| Can define default            |br|| No         | Yes        | El constructor predeterminado        |br||
| constructor?                      |            |            | inicializa struct todos los campos   |br||
|                                   |            |            | de instancia a los valores por       |br||
|                                   |            |            | defecto y no se puede cambiar.           |
+-----------------------------------+------------+------------+------------------------------------------+
| Can overload operators?           | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can be generic?                   | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can be partial?                   | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| Can be sealed?                    | Always     | Yes        | Las estructuras siempre están        |br||
|                                   |            |            | sellados y no se pueden tener        |br||
|                                   |            |            | structs derivadas.                       |
+-----------------------------------+------------+------------+------------------------------------------+
| Can be referenced in instance     | Yes        | Yes        |                                          |
+-----------------------------------+------------+------------+------------------------------------------+
| members using this            |br|| No         | Yes        | Clases de C # deben instanciar       |br||
| keyword? Needs new            |br||            |            | usando new. Sin embargo, las         |br||
| operator to create            |br||            |            | estructuras no requieren esto.       |br||
| instance?                         |            |            | Mientras que New se puede utilizar   |br||
|                                   |            |            | en una estructura que llamar a un    |br||
|                                   |            |            | constructor, puede optar por no      |br||
|                                   |            |            | utilizar new e init los campos a ti  |br||
|                                   |            |            | mismo, pero hay que init todos los   |br||
|                                   |            |            | campos y los campos debe ser público!    |
+-----------------------------------+------------+------------+------------------------------------------+
