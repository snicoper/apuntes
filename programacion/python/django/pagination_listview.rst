.. _reference-programacion-python-django-pagination_listview:

######################
Pagination en ListView
######################

**Fuentes**

* https://djangosnippets.org/snippets/3023/

------

En ``views.py``

.. code-block:: python

    # myapp/views.py
    class MyModelListView(ListView):
        model = MyModel
        template_name = 'myapp/my_template.html'
        paginate_by = 10


En ``templates/my_template.html``

.. code-block:: htmldjango

    <!-- myapp/templates/my_template.html -->

    <nav>
        {% if is_paginated %}
            <ul class="pagination">
                {% if page_obj.has_previous %}
                    <li><a href="?page={{ page_obj.previous_page_number }}">&laquo;</a></li>
                {% endif %}

                {% for i in paginator.page_range %}
                    <li {% if page_obj.number == i %} class="active" {% endif %}>
                        <a href="?page={{i}}">{{ i }}</a>
                    </li>
                {% endfor %}

                {% if page_obj.has_next %}
                    <li><a href="?page={{ page_obj.next_page_number }}">&raquo;</a></li>
                {% endif %}
            </ul>
        {% endif %}
    </nav>
