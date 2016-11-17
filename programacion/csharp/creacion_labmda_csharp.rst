.. _reference-programacion-csharp-creacion_labmda_csharp:

#########################################
Creacion de un metodo con un param lambda
#########################################

**Fuentes**

* `OrtizOL - Experiencias Construcción Software (xCSw) <http://ortizol.blogspot.com.es/2014/06/expresiones-lambda-en-csharp-parte-1-introduccion-a-las-expresiones-lambda.html?q=lambda>`_

----

Me dejo un ejemplo para recordar.

.. code-block:: c#

    using System;
    using System.Collections.Generic;

    namespace ConsolePracticas
    {
        class Program
        {
            static void Main(string[] args)
            {
                List<Person> persons = new List<Person>
                {
                    new Person { Id = 1, Nombre = "snicoper" },
                    new Person { Id = 2, Nombre = "perico" },
                    new Person { Id = 3, Nombre = "palote" },
                };

                IEnumerable<Person> query = persons.MyWhere(p => p.Id > 1);

                foreach (Person ele in query)
                {
                    Console.Write("{0}, ", ele.Nombre); // perico, palote,
                }

                Console.ReadLine();
            }
        }

        public static class MyExtensions
        {
            public static IEnumerable<T> MyWhere<T>(this IEnumerable<T> lista, Func<T, bool> predicate)
            {
                foreach (T element in lista)
                {
                    if (predicate(element))
                    {
                        yield return element;
                    }
                }
            }
        }

        public class Person
        {
            public int Id { get; set; }
            public string Nombre { get; set; }
        }
    }
