.. _reference-programacion-csharp-ienumerator:

###########
IEnumerator
###########

Pequeño ejemplo que implementa IEnumerator con genéricos.

.. code-block:: c#

    class IntList<T> : IEnumerable<T>
    {
        private int count = 0;
        private T[] values;

        public int Count { get { return count; } }

        public IntList(int capacity)
        {
            values = new T[capacity];
        }

        public void Add(T value)
        {
            values[count] = value;
            count++;
        }

        public T this[int index]
        {
            get { return values[index]; }
            set { values[index] = value; }
        }

        public IEnumerator<T> GetEnumerator()
        {
            for (int i = 0; i < count; i++)
            {
                yield return values[i];
            }
        }

        IEnumerator IEnumerable.GetEnumerator()
        {
            return GetEnumerator();
        }
    }
