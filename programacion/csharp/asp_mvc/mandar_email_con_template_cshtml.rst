.. _reference-programacion-asp_mvc-mandar_email_con_template_cshtml:

#############################
Mandar Email con View .cshtml
#############################

Mandar un email con un template ``.cshtml``.

Crear directorio ``~/Views/TemplateEmails``

Crear archivo ``~/Views/TemplateEmails/_LayoutEmail.cshtml``

.. code-block:: HTML

    @{
        Layout = null;
    }

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>@ViewBag.Title - My ASP.NET Application</title>
    </head>
    <body>
        <div>
            @RenderBody()
        </div>
    </body>
    </html>

Este sera el **Layout** por defecto para los emails. Luego una **View** para un email, sera algo asi:

.. code-block:: html

    @{
        ViewBag.Title = "Contact";
        Layout = "~/Views/TemplateEmails/_LayoutEmail.cshtml";
    }

    <h2>Contact</h2>

    <!-- resto del html, todo igual a las Views con Razor, con using, model, etc. -->

Editar ``~/Global.asax.cs/`` y en el metodo ``Application_Start`` añadir:

.. code-block:: csharp

    // Añadir ~/Views/TemplateEmails a razor engine.
    RazorViewEngine razorEngine = ViewEngines.Engines.OfType<RazorViewEngine>().FirstOrDefault();
    razorEngine.ViewLocationFormats = razorEngine.ViewLocationFormats.Concat(
        new string[] { "~/Views/TemplateEmails/{0}.cshtml" }
    ).ToArray();

    // Partials en ~/Views/TemplateEmails
    razorEngine.PartialViewLocationFormats = razorEngine.PartialViewLocationFormats.Concat(
        new string[] { "~/Views/TemplateEmails/{0}.cshtml" }
    ).ToArray();

Para el ejemplo creo el directorio ``~/Core`` y dentro creo el archivo ``ViewRenderer.cs`` con el
siguiente código de https://gist.github.com/HarveyWilliams/0405edd6719c16171329

.. code-block:: csharp

    using System;
    using System.Web;
    using System.Web.Mvc;
    using System.IO;
    using System.Web.Routing;

    namespace WebApplication1.Core
    {
        /// <summary>
        /// Class that renders MVC views to a string using the
        /// standard MVC View Engine to render the view.
        ///
        /// Requires that ASP.NET HttpContext is present to
        /// work, but works outside of the context of MVC
        ///
        /// Particularly useful for rendering CSHTML for emails.
        ///
        /// Code extracted from:
        /// https://github.com/RickStrahl/WestwindToolkit/blob/master/Westwind.Web.Mvc/Utils/ViewRenderer.cs
        /// </summary>
        public class ViewRenderer
        {
            /// <summary>
            /// Required Controller Context
            /// </summary>
            protected ControllerContext Context { get; set; }

            /// <summary>
            /// Initializes the ViewRenderer with a Context.
            /// </summary>
            /// <param name="controllerContext">
            /// If you are running within the context of an ASP.NET MVC request pass in
            /// the controller's context.
            /// Only leave out the context if no context is otherwise available.
            /// </param>
            public ViewRenderer(ControllerContext controllerContext = null)
            {
                // Create a known controller from HttpContext if no context is passed
                if (controllerContext == null)
                {
                    if (HttpContext.Current != null)
                        controllerContext = CreateController<EmptyController>().ControllerContext;
                    else
                        throw new InvalidOperationException(
                            "ViewRenderer must run in the context of an ASP.NET " +
                            "Application and requires HttpContext.Current to be present.");
                }
                Context = controllerContext;
            }

            /// <summary>
            /// Renders a full MVC view to a string. Will render with the full MVC
            /// View engine including running _ViewStart and merging into _Layout
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to render the view with</param>
            /// <returns>String of the rendered view or null on error</returns>
            public string RenderViewToString(string viewPath, object model = null)
            {
                return RenderViewToStringInternal(viewPath, model, false);
            }

            /// <summary>
            /// Renders a full MVC view to a writer. Will render with the full MVC
            /// View engine including running _ViewStart and merging into _Layout
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to render the view with</param>
            /// <returns>String of the rendered view or null on error</returns>
            public void RenderView(string viewPath, object model, TextWriter writer)
            {
                RenderViewToWriterInternal(viewPath, writer, model, false);
            }


            /// <summary>
            /// Renders a partial MVC view to string. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <returns>String of the rendered view or null on error</returns>
            public string RenderPartialViewToString(string viewPath, object model = null)
            {
                return RenderViewToStringInternal(viewPath, model, true);
            }

            /// <summary>
            /// Renders a partial MVC view to given Writer. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="writer">Writer to render the view to</param>
            public void RenderPartialView(string viewPath, object model, TextWriter writer)
            {
                RenderViewToWriterInternal(viewPath, writer, model, true);
            }

            /// <summary>
            /// Renders a partial MVC view to string. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="controllerContext">Active Controller context</param>
            /// <returns>String of the rendered view or null on error</returns>
            public static string RenderView(string viewPath, object model = null,
                                            ControllerContext controllerContext = null)
            {
                ViewRenderer renderer = new ViewRenderer(controllerContext);
                return renderer.RenderViewToString(viewPath, model);
            }

            /// <summary>
            /// Renders a partial MVC view to the given writer. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="writer">Writer to render the view to</param>
            /// <param name="controllerContext">Active Controller context</param>
            /// <returns>String of the rendered view or null on error</returns>
            public static void RenderView(string viewPath, TextWriter writer, object model,
                                            ControllerContext controllerContext)
            {
                ViewRenderer renderer = new ViewRenderer(controllerContext);
                renderer.RenderView(viewPath, model, writer);
            }

            /// <summary>
            /// Renders a partial MVC view to string. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="controllerContext">Active Controller context</param>
            /// <param name="errorMessage">optional out parameter that captures an error message instead of throwing</param>
            /// <returns>String of the rendered view or null on error</returns>
            public static string RenderView(string viewPath, object model,
                                            ControllerContext controllerContext,
                                            out string errorMessage)
            {
                errorMessage = null;
                try
                {
                    ViewRenderer renderer = new ViewRenderer(controllerContext);
                    return renderer.RenderViewToString(viewPath, model);
                }
                catch (Exception ex)
                {
                    errorMessage = ex.GetBaseException().Message;
                }
                return null;
            }

            /// <summary>
            /// Renders a partial MVC view to the given writer. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="controllerContext">Active Controller context</param>
            /// <param name="writer">Writer to render the view to</param>
            /// <param name="errorMessage">optional out parameter that captures an error message instead of throwing</param>
            /// <returns>String of the rendered view or null on error</returns>
            public static void RenderView(string viewPath, object model, TextWriter writer,
                                            ControllerContext controllerContext,
                                            out string errorMessage)
            {
                errorMessage = null;
                try
                {
                    ViewRenderer renderer = new ViewRenderer(controllerContext);
                    renderer.RenderView(viewPath, model, writer);
                }
                catch (Exception ex)
                {
                    errorMessage = ex.GetBaseException().Message;
                }
            }


            /// <summary>
            /// Renders a partial MVC view to string. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="controllerContext">Active controller context</param>
            /// <returns>String of the rendered view or null on error</returns>
            public static string RenderPartialView(string viewPath, object model = null,
                                                    ControllerContext controllerContext = null)
            {
                ViewRenderer renderer = new ViewRenderer(controllerContext);
                return renderer.RenderPartialViewToString(viewPath, model);
            }

            /// <summary>
            /// Renders a partial MVC view to string. Use this method to render
            /// a partial view that doesn't merge with _Layout and doesn't fire
            /// _ViewStart.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">The model to pass to the viewRenderer</param>
            /// <param name="controllerContext">Active controller context</param>
            /// <param name="writer">Text writer to render view to</param>
            /// <param name="errorMessage">optional output parameter to receive an error message on failure</param>
            public static void RenderPartialView(string viewPath, TextWriter writer, object model = null,
                                                    ControllerContext controllerContext = null)
            {
                ViewRenderer renderer = new ViewRenderer(controllerContext);
                renderer.RenderPartialView(viewPath, model, writer);
            }


            /// <summary>
            /// Internal method that handles rendering of either partial or
            /// or full views.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">Model to render the view with</param>
            /// <param name="partial">Determines whether to render a full or partial view</param>
            /// <param name="writer">Text writer to render view to</param>
            protected void RenderViewToWriterInternal(string viewPath, TextWriter writer, object model = null, bool partial = false)
            {
                // first find the ViewEngine for this view
                ViewEngineResult viewEngineResult = null;
                if (partial)
                    viewEngineResult = ViewEngines.Engines.FindPartialView(Context, viewPath);
                else
                    viewEngineResult = ViewEngines.Engines.FindView(Context, viewPath, null);

                if (viewEngineResult == null)
                    throw new FileNotFoundException();

                // get the view and attach the model to view data
                var view = viewEngineResult.View;
                Context.Controller.ViewData.Model = model;

                var ctx = new ViewContext(Context, view,
                                            Context.Controller.ViewData,
                                            Context.Controller.TempData,
                                            writer);
                view.Render(ctx, writer);
            }

            /// <summary>
            /// Internal method that handles rendering of either partial or
            /// or full views.
            /// </summary>
            /// <param name="viewPath">
            /// The path to the view to render. Either in same controller, shared by
            /// name or as fully qualified ~/ path including extension
            /// </param>
            /// <param name="model">Model to render the view with</param>
            /// <param name="partial">Determines whether to render a full or partial view</param>
            /// <returns>String of the rendered view</returns>
            private string RenderViewToStringInternal(string viewPath, object model,
                                                        bool partial = false)
            {
                // first find the ViewEngine for this view
                ViewEngineResult viewEngineResult = null;
                if (partial)
                    viewEngineResult = ViewEngines.Engines.FindPartialView(Context, viewPath);
                else
                    viewEngineResult = ViewEngines.Engines.FindView(Context, viewPath, null);

                if (viewEngineResult == null || viewEngineResult.View == null)
                {
                    //throw new FileNotFoundException(Resources.ViewCouldNotBeFound);
                    throw new Exception("Can't find view.");
                }

                // get the view and attach the model to view data
                var view = viewEngineResult.View;
                Context.Controller.ViewData.Model = model;

                string result = null;

                using (var sw = new StringWriter())
                {
                    var ctx = new ViewContext(Context, view,
                                                Context.Controller.ViewData,
                                                Context.Controller.TempData,
                                                sw);
                    view.Render(ctx, sw);
                    result = sw.ToString();
                }

                return result;
            }


            /// <summary>
            /// Creates an instance of an MVC controller from scratch
            /// when no existing ControllerContext is present
            /// </summary>
            /// <typeparam name="T">Type of the controller to create</typeparam>
            /// <returns>Controller for T</returns>
            /// <exception cref="InvalidOperationException">thrown if HttpContext not available</exception>
            public static T CreateController<T>(RouteData routeData = null, params object[] parameters)
                        where T : Controller, new()
            {
                // create a disconnected controller instance
                T controller = (T)Activator.CreateInstance(typeof(T), parameters);

                // get context wrapper from HttpContext if available
                HttpContextBase wrapper = null;
                if (HttpContext.Current != null)
                    wrapper = new HttpContextWrapper(System.Web.HttpContext.Current);
                else
                    throw new InvalidOperationException(
                        "Can't create Controller Context if no active HttpContext instance is available.");

                if (routeData == null)
                    routeData = new RouteData();

                // add the controller routing if not existing
                if (!routeData.Values.ContainsKey("controller") && !routeData.Values.ContainsKey("Controller"))
                    routeData.Values.Add("controller", controller.GetType().Name
                                                                .ToLower()
                                                                .Replace("controller", ""));

                controller.ControllerContext = new ControllerContext(wrapper, routeData, controller);
                return controller;
            }

        }

        /// <summary>
        /// Empty MVC Controller instance used to
        /// instantiate and provide a new ControllerContext
        /// for the ViewRenderer
        /// </summary>
        public class EmptyController : Controller
        {
        }
    }

Dentro de ``~/Core`` creo ``SimpleEmail.cs``

.. code-block:: csharp

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Net;
    using System.Net.Mail;
    using System.Threading.Tasks;

    namespace WebApplication1.Core.Emails
    {
        /// <summary>
        /// Envía un email renderizando con Razor engine.
        ///
        /// Ejemplo:
        /// var template = "Hello";
        /// var subject = "Email de prueba";
        /// var from = new MailAddress("perico@example.com"); //Opcional || SMTPDefaultFrom
        /// var to = new List<MailAddress> { new MailAddress("palote@example.com") };
        /// var model = new Person { Username = "Perico de los Palotes", Email = "perico@example.com" }; // Opcional
        /// SimpleEmail.Send(template, subject, from, to, model);
        ///
        /// Require:
        ///
        /// https://gist.github.com/HarveyWilliams/0405edd6719c16171329
        ///
        /// Web.config en appSettings
        ///
        /// <add key="SMTPDefaultFromName" value="My Company"/>
        /// <add key="SMTPDefaultFromEmail" value="default@example.com"/>
        /// <add key="SMTPHost" value="smtp.gmail.com"/>
        /// <add key="SMTPEnableSsl" value="true"/>
        /// <add key="SMTPUserName" value="username@gmail.com"/>
        /// <add key="SMTPPassword" value="MI_PASSWORD"/>
        /// <add key="SMTPPort" value="587" />
        /// </summary>
        public class SimpleEmail : IDisposable
        {
            /// <summary>
            /// Template para el email.
            /// </summary>
            private string _template;

            /// <summary>
            /// Titulo del email.
            /// </summary>
            private string _subject;

            /// <summary>
            /// Cabecera FROM:
            /// </summary>
            private MailAddress _from;

            /// <summary>
            /// Lista de emails destinatarios.
            /// </summary>
            private List<MailAddress> _to;

            /// <summary>
            /// ¿El email sera enviado como HTML?
            /// </summary>
            private bool _isBodyHtml;

            /// <summary>
            /// Cuerpo del email.
            /// </summary>
            private string _body;

            /// <summary>
            /// model para la View.
            /// </summary>
            private object _model;

            // SMTP
            private MailMessage _mailMessage;
            private NetworkCredential _networkCredential;
            private SmtpClient _smtpClient;

            /// <summary>
            /// Envía un email asíncrono.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">Cabeceras para From:</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="model">model para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static async Task SendAsync(string template, string subject, MailAddress from, List<MailAddress> to, object model = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, from, to, model, isBodyHtml);
                await email._smtpClient.SendMailAsync(email._mailMessage);
            }

            /// <summary>
            /// Envía un email asíncrono.<br>
            /// El campo From: lo obtendrá de SMTPDefaultFrom del archivo de configuración.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="model">model para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static async Task SendAsync(string template, string subject, List<MailAddress> to, object model = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, null, to, model, isBodyHtml);
                await email._smtpClient.SendMailAsync(email._mailMessage);
            }

            /// <summary>
            /// Envía un email.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">Cabeceras para From:</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="model">model para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static void Send(string template, string subject, MailAddress from, List<MailAddress> to, object model = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, from, to, model, isBodyHtml);
                email._smtpClient.Send(email._mailMessage);
            }

            /// <summary>
            /// Envía un email.<br>
            /// El campo From: lo obtendrá de SMTPDefaultFrom del archivo de configuración.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="model">model para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static void Send(string template, string subject, List<MailAddress> to, object model = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, null, to, model, isBodyHtml);
                email._smtpClient.Send(email._mailMessage);
            }

            /// <summary>
            /// Solo es instanciable desde los métodos statics
            /// </summary>
            private SimpleEmail()
            {
                _mailMessage = new MailMessage();

                _networkCredential = new NetworkCredential()
                {
                    UserName = ConfigurationManager.AppSettings["SMTPUserName"],
                    Password = ConfigurationManager.AppSettings["SMTPPassword"]
                };

                _smtpClient = new SmtpClient()
                {
                    Host = ConfigurationManager.AppSettings["SMTPHost"],
                    EnableSsl = Convert.ToBoolean(ConfigurationManager.AppSettings["SMTPEnableSsl"]),
                    UseDefaultCredentials = true,
                    Credentials = _networkCredential,
                    Port = int.Parse(ConfigurationManager.AppSettings["SMTPPort"])
                };
            }

            /// <summary>
            /// Obtener instancia.
            /// </summary>
            private static SimpleEmail _getInstance(string template, string subject, MailAddress from, List<MailAddress> to, object model, bool isBodyHtml)
            {
                from = from ?? new MailAddress(
                    ConfigurationManager.AppSettings["SMTPDefaultFromEmail"],
                    ConfigurationManager.AppSettings["SMTPDefaultFromName"]
                );

                SimpleEmail email = new SimpleEmail
                {
                    _template = template,
                    _subject = subject,
                    _from = from,
                    _to = to,
                    _model = model
                };
                email._isBodyHtml = isBodyHtml;
                email._render();
                email._initialize();
                return email;
            }

            /// <summary>
            /// Inicializa las variables de clase.
            /// </summary>
            private void _initialize()
            {
                _mailMessage.From = _from;
                _mailMessage.Subject = _subject;
                _mailMessage.Body = _body;
                _mailMessage.IsBodyHtml = _isBodyHtml;

                foreach (var m in _to)
                {
                    _mailMessage.To.Add(m);
                }
            }

            /// <summary>
            /// Renderiza el archivo con Razor.
            /// </summary>
            private string _render()
            {
                _body = ViewRenderer.RenderView(_template, _model);
                return _body;
            }

            public void Dispose()
            {
                _smtpClient.Dispose();
                _mailMessage.Dispose();
            }
        }
    }

En el archivo ``Web.config``

.. code-block:: xml

    <appSettings>
        <!-- ... --->
        <add key="SMTPDefaultFromName" value="My Company"/>
        <add key="SMTPDefaultFromEmail" value="default@example.com"/>
        <add key="SMTPHost" value="smtp.gmail.com"/>
        <add key="SMTPEnableSsl" value="true"/>
        <add key="SMTPUserName" value="username@gmail.com"/>
        <add key="SMTPPassword" value="MI_PASSWORD"/>
        <add key="SMTPPort" value="587" />
    </appSettings>
