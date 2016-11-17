.. _reference-programacion-csharp-csharp_script-calcular_tiempo_ejecucion:

###########################################
Calcular Tiempo de Ejecución de un Programa
###########################################

.. code-block:: c#

    using System.Diagnogtics;


    Stopwatch sw = new Stopwatch();
    sw.Start();

    // También se puede inicializar con un método static Stopwatch sw = Stopwatch.StartNew();

    int contador = 0;
    for (int i = 0; i < 27; i++)
    {
        for (int j = 0; j < 27; j++)
        {
            for (int k = 0; k < 22; k++)
            {
                for (int g = 0; g < 100000; g++)
                {
                    contador++;
                }
            }
        }
    }

    Console.WriteLine(contador);

    sw.Stop();
    Console.WriteLine(sw.Elapsed.TotalSeconds);
