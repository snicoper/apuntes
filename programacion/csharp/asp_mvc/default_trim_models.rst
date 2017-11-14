.. _reference-programacion-asp_mvc-default_trim_models:

############################
Trim los modelos por defecto
############################

Para que al guardar un modelo, todos los campos quitarles los espacios delete y detras.

Crear ``TrimModelBinder.cs``, en ``Core`` y añadir:

.. code-block:: csharp

    using System.ComponentModel;
    using System.Web.Mvc;

    namespace NAMESPACE.Core
    {
        /// <summary>
        /// Por defecto los modelos elimina los espacios en blanco.
        /// </summary>
        public class TrimModelBinder : DefaultModelBinder
        {
            protected override void SetProperty(ControllerContext controllerContext, ModelBindingContext bindingContext,
                                                PropertyDescriptor propertyDescriptor, object value)
            {
                if (propertyDescriptor.PropertyType == typeof(string))
                {
                    var stringValue = (string)value;
                    if (!string.IsNullOrWhiteSpace(stringValue))
                    {
                        value = stringValue.Trim();
                    }
                    else
                    {
                        value = null;
                    }
                }
                base.SetProperty(controllerContext, bindingContext, propertyDescriptor, value);
            }
        }
    }

Ponerlo por defecto en ``Global.asax`` en el método ``Application_Start``

.. code-block:: csharp

    protected void Application_Start()
    {
        AreaRegistration.RegisterAllAreas();
        RouteConfig.RegisterRoutes(RouteTable.Routes);

        // Trim en los modelos por defecto.
        ModelBinders.Binders.DefaultBinder = new TrimModelBinder();

        // ...
    }
