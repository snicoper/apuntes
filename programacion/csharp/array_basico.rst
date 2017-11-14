.. _reference-programacion-csharp-array_basico:

############
Array Básico
############

Arrays una dimensión
********************

Declarar e inicializar un array:

.. code-block:: c#

    // Crear un array con 10 elementos sin rellenarlos
    string[] myArray = new string[10];

    // Para asignar valores usar indices en los []
    myArray[0] = "elemento";

    // Crear array e insertarle valores
    int[] myArray = {1, 2, 3, 4, 5};

    // Es equivalente a:
    int[] myArray = new int[5] {1, 2, 3, 4, 5};

    // o
    int[] myArray = new int[5];
    myArray[0] = 1;
    myArray[1] = 2;
    myArray[2] = 3;
    myArray[3] = 4;
    myArray[4] = 5;

Multidimensional Arrays
***********************

Son arrays de dos dimensiones, se puede pensar en ellas (siendo de 2 dimensiones)
como filas y columnas en una tabla.

Para declarar una se usa la siguiente sintaxis:

.. code-block:: c#

    int[,] matrix = new int[4, 2];

Esto crea una "tabla mas o menos así"

.. code-block:: bash

    x x
    x x
    x x
    x x

Una manera rápida seria:

.. code-block:: c#

    int[,] matrix = { {1, 1}, {2, 2}, {3, 5}, {4, 5} };

Donde:

.. code-block:: bash

    1 1
    2 2
    3 5
    4 5

    matrix[0, 2]; // 3
    matrix[1, 2]; // 5

Arrays de Arrays
****************

También llamadas arrays escalonada, ya que cada fila puede tener un numero x de elementos.

Un ejemplo rápido:

.. code-block:: c#

    int[][] matrix = new int[3][];
    matrix[0] = new int[5];
    matrix[1] = new int[4];
    matrix[2] = new int[2];
    matrix[0][3] = 4;
    matrix[1][1] = 8;
    matrix[2][0] = 5;

.. code-block:: bash

    0 0 0 4 0
    0 8 0 0
    5 0

Los elementos que no se hayan inicializado, su valor sera null, independientemente
del tipo al que pertenezca el elemento.

.. code-block:: c#

    string[] nombres = new string[10];
    int[] numeros = new int[10];

    nombres[1]; // null
    numeros[1]; // null
