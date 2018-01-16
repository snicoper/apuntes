.. _reference-programacion-csharp-dotnet_core-tempdata_messages:

########################################
Mensajes TempData con bootstrap y toastr
########################################

Esta es una forma cómoda para crear mensajes con `TempData`.

Para el apunte se usa por un lado toastr_ y por otro
bootstrap4_

.. _toastr: https://github.com/CodeSeven/toastr

.. _bootstrap4: https://getbootstrap.com/

Primero se crea una **clase de extension** de ``Controller``

.. code-block:: csharp

    public static class TempDataMessage
    {
        public static void AddMessage(this Controller controller, string identifier, string message)
        {
            if (controller.TempData.ContainsKey("messages"))
            {
                (controller.TempData["messages"] as Dictionary<string, string>).Add(identifier, message);
            }
            else
            {
                controller.TempData["messages"] = new Dictionary<string, string>
                {
                    [identifier] = message
                };
            }
        }

        public static void AddMessageFixed(this Controller controller, string identifier, string message)
        {
            if (controller.TempData.ContainsKey("messagesFixed"))
            {
                (controller.TempData["messagesFixed"] as Dictionary<string, string>).Add(identifier, message);
            }
            else
            {
                controller.TempData["messagesFixed"] = new Dictionary<string, string>
                {
                    [identifier] = message
                };
            }
        }
    }

Desde un controlador ahora se podrán crear mensajes, el método ``AddMessage`` añadirá uno para ``toastr``
y ``AddMessageFixed`` para Bootstrap4 (aunque cambiando las vistas podrá mostrar de la forma que cada
uno quiera.

Creamos ahora 2 views en ``Views/Shared/``, ``_Messages.cshtml`` y ``_MessagesFixed.cshtml``

.. code-block:: html

    <!-- _Messages.cshtml -->
    @model Dictionary<string, string>

    @if (Model != null)
    {
      @foreach (var message in Model)
      {
        <script>
          toastr['@message.Key']('@message.Value')
        </script>
      }
    }

.. code-block:: html

    <!-- _MessagesFixed.cshtml -->
    @model Dictionary<string, string>

    @if (Model != null)
    {
      <div class="row">
        <div class="col-8 m-auto">
          @foreach (var message in Model)
          {
            <div class="alert alert-@message.Key alert-dismissible fade show" role="alert">
              @message.Value
              <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
          }
        </div>
      </div>
    }

Editar ``_Layout.cshtml``

.. code-block:: html

    <!-- Añadirlo donde se quieren mostrar los mensajes de Bootstrap4 -->
    @Html.Partial("_MessagesFixed", (Dictionary<string, string>)TempData["messagesFixed"])

    <!-- Añadirlo después de tener cargada la librería toastr -->
    @Html.Partial("_Messages", (Dictionary<string, string>)TempData["messages"])

Comprobar desde un `Action`

.. code-block:: csharp

    public IActionResult Index()
    {
        this.AddMessage("success", "Un mensaje de prueba");
        this.AddMessage("info", "Un mensaje de prueba");
        this.AddMessageFixed("success", "Un mensaje de prueba");
        this.AddMessageFixed("info", "Un mensaje de prueba");
        return View();
    }
