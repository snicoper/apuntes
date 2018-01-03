.. _reference-programacion-csharp-dotnet_core-css_fields_error:

###########################
Campos formulario error css
###########################

Típico campo de formulario.

.. code-block:: html

    <div class="form-group">
      <label asp-for="Name">Your name:</label>
      <input asp-for="Name" class="form-control">
      <span asp-validation-for="Name" class="small"></span>
    </div>

Añadir en el archivo ``main.css``, modificar al gusto del consumidor.

.. code-block:: css

    .field-validation-error    {color: #dc3545;}
    .field-validation-valid    { display: none;}
    .input-validation-error    { border: 1px solid #dc3545; }
    .validation-summary-valid  { display: none;}
    .validation-summary-errors { color: #dc3545; }
    .validation-summary-errors ul {
        list-style: none;
        padding: 0.5rem;
        border: 1px solid #dc3545;
        background-color: #ffebee;
    }
