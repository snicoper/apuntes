####################
Django templateforms
####################

Templates para [Materializecss](http://materializecss.com), pero facilmente se pueden añadir para otros frameworks css.

Uso
===

Cargar las ``tags`` al principio del template.

.. code-block:: htmldjango

    {% load templateforms %}

La manera mas rápida de usarla es con el tag ``form`` pasando como parámetro el formulario.

.. code-block:: htmldjango

    <form method="post" action="">
      {% csrf_token %}
      {% form form %}
      <button type="submit">Submit</button>
    </form>

Si se quiere omitir el ``*`` cuando el campo es requerido ``{% form form hidden_required='1' %}``

.. code-block:: htmldjango

    <form method="post" action="">
      {% csrf_token %}
      {% form form hidden_required='1' %}
      <button type="submit">Submit</button>
    </form>

Campo a campo
=============

Otra manera es pasando cada campo del formulario, pudiendo pasar parámetros.

.. code-block:: htmldjango

    <form method="post" action="">
      {% csrf_token %}

      {# Mostrar errores globales del formulario #}
      {% non_field_errors form.non_field_errors %}

      {# Campos ocultos #}
      {% form_hidden_fields form.hidden_fields %}

      {# Campos del formulario #}
      {% form_field form.myfield label='My Field' %}
      <button type="submit">Submit</button>
    </form>

Parámetros
==========

Globales
********

Estos parámetros los acepta todos los campos.

``col``: Es el campo ``col`` en **materializecss**

.. code-block:: htmldjango

    <div class="row">
        <!-- Materializecss -->
        {% form_field form.myfield col='s12 m12 l6' %}
    </div>

Pondrá en ``large`` un campo al lado del otro. Requiere envolverlo en un ``div`` (u otro contenedor) con ``class="row"``.

Si se omite, envolverá internamente el campo en un ``<div class="row"><div class="col s12">``.

``tpl_name``: Omite el template del **tipo de campo** por defecto.

.. code-block:: console

    {% form_field form.myfield tpl_name='mistemplates/mitemplate.html' %}

``label``: Nombre a mostrar

.. code-block:: htmldjango

    {% form_field form.myfield label="Mi label personalizado" %}

Si se omite, usara ``form.myfield.label``

Todos los campos añade el valor de ``help_text`` del model o form, si lo tiene.

.. code-block:: htmldjango

    <span class="help_text">{{ field.help_text }}</span>

Todos los campos añade ``{{ field.errors }}`` (es el de django por defecto)

.. code-block:: htmldjango

    <ul class="errorlist"><li>This field is required.</li></ul>

Type text
*********

Los campos de tipo texto como ``text``, ``email``, ``number``, ``date``, ``password``, ``url``, etc, aceptan los siguientes parámetros.

``ftype``: Para cambiar el ``type=""``, por defecto ``text``

Internamente, ya añade un ``type`` adecuado, pero si algún campo no lo he puesto, es posible ponerlo desde estos parámetros.

``img``: Añade una imagen a la izquierda del campo (**materializecss**).

TODO: No lo hace en todos los campos, por hacer...

**Requiere las fuentes de material icons**

.. code-block:: htmldjango

    <!-- en base.html -->
    <link rel="stylesheet" href="http://fonts.googleapis.com/icon?family=Material+Icons">

    <!-- en cualquier plantilla donde se este creando el form -->
    {% form_field form.myfield img="account_circle" %}

Cualquier imagen de [material icons](https://design.google.com/icons/) pasando el en nombre.

No incluye ningun Javascript, por lo que si el campo lo require, se debera añadir a parte, como por ejemplo los campos ``select``

.. code-block:: javascript

    $(document).ready(function() {
      $('select').material_select();
    });
