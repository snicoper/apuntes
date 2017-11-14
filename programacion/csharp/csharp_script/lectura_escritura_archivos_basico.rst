.. _reference-programacion-csharp-csharp_script-lectura_escritura_archivos_basico:

#################################
Lectura Escritura archivos Básico
#################################

Fuentes
*******

* http://msdn.microsoft.com/es-es/library/system.io.filestream%28v=vs.110%29.aspx

-------------

``using System.IO``

Comprobar si un archivo existe
******************************

.. code-block:: c#

    if (!File.Exists(filePath))
    {
        throw new FileNotFoundException();
    }

Escribir en un archivo
**********************

Si existe, y lo que queremos hacer es escribir en el:

.. code-block:: c#

    using (FileStream fs = new FileStream(filePath, FileMode.Open, FileAccess.Write))
    {

    }

Con FileMode, decimos el modo de abrir el archivo, ejemplo, Append, OpenOrCreate, etc.

http://msdn.microsoft.com/es-es/library/system.io.filemode%28v=vs.110%29.aspx

Con FileAccess, decimos el acceso al archivo, ejemplo, Read, ReadWrite o Write.

Pienso que es la mejor manera de abrir un recurso, por que podemos decirle el
modo y acceso al recurso.

Ahora con StreamWriter, añadimos los datos.
Cuando se usan varios recursos, es posible poner uno seguido del otro, como en el
siguiente ejemplo.
El compilador generará los bloques try-finally anidados apropiados.


.. code-block:: c#

    using (FileStream fs = new FileStream(archivo, FileMode.OpenOrCreate, FileAccess.Write))
    using (StreamWriter sw = new StreamWriter(fs))
    {
        sw.Write("Nuevo texto");
        sw.WriteLine("Nueva linea");
    }

Leer de un archivo
******************

También es posible abrirlo con FileStream, pero como solo se trata de leerlo, también
lo puedo hacer con StreamReader.

Primero, seria comprobar si el archivo existe y en caso de existir, abrirlo

.. code-block:: c#

    using (StreamReader sr = new StreamReader(filePath))
    {
        //Leer el archivo
    }
