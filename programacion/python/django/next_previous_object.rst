.. _reference-programacion-python-django-next_previous_object:

#####################################################
Obtener el anterior y el siguiente del objeto actual.
#####################################################

**Fuentes**

* https://docs.djangoproject.com/en/dev/ref/models/instances/#django.db.models.Model.get_next_by_FOO

--------------

Desde las views
***************

Preparar las variables de contexto en las ``views``

.. code-block:: python

    class ArticleDetailView(generic.DetailView):

        """
        Detalles de un articulo.
        """
        template_name = 'blog/article_detail.html'
        model = Article
        context_object_name = 'article'

        def get_context_data(self, **kwargs):
            context = super(ArticleDetailView, self).get_context_data(**kwargs)
            # Obtener el anterior y siguiente articulo.
            try:
                context['article_previous'] = self.get_object().get_previous_by_create_at()
            except:
                context['article_previous'] = None
            try:
                context['article_next'] = self.get_object().get_next_by_create_at()
            except:
                context['article_next'] = None
            return context

Y utilizarlas desde los templates.

.. code-block:: html

    <nav class="paginated">
      <div class="row">
        <div class="col-sm-6">
          {% if article_previous %}
            <a href="{% url 'blog.article_detail' article_previous.slug %}">
              <span class="glyphicon glyphicon-chevron-left"></span>
              {{ article_previous }}
            </a>
          {% endif %}
        </div>
        <div class="col-sm-6 text-right">
          {% if article_next %}
            <a href="{% url 'blog.article_detail' article_next.slug %}">
              {{ article_next }}
              <span class="glyphicon glyphicon-chevron-right"></span>
            </a>
          {% endif %}
        </div>
      </div>
    </nav>

Desde los templates
*******************

Ha diferencia del anterior es mas directo (El ejemplo es un poco distinto por marco css, etc.).

Aquí no es necesario preparar las variables de contexto.

.. code-block:: html

    {% with article_previous=article.get_previous_by_create_at %}
      {% if article_previous %}
        <div class="article-previous">
          <a class="btn waves-effect tooltipped"
             data-position="bottom"
             data-delay="50"
             data-tooltip="{{ article_previous.title }}"
             href="{% url 'blog:article_detail' article_previous.slug %}"
          >
            <i class="fa fa-caret-left" aria-hidden="true"></i> {{ article_previous.title|truncatewords:3 }}
          </a>
        </div>
      {% endif %}
    {% endwith %}

    {% with article_next=article.get_next_by_create_at %}
      {% if article_next %}
        <div class="article-next">
          <a class="btn waves-effect tooltipped"
             data-position="bottom"
             data-delay="50"
             data-tooltip="{{ article_next.title }}"
             href="{% url 'blog:article_detail' article_next.slug %}"
          >
            {{ article_next.title|truncatewords:3 }} <i class="fa fa-caret-right" aria-hidden="true"></i>
          </a>
        </div>
      {% endif %}
    {% endwith %}
