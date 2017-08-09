.. _reference-programacion-asp_mvc-mandar_email_con_template_cshtml:

#############################
Mandar Email con View .cshtml
#############################

Mandar un email con un template ``.cshtml`` o ``.txt``

.. code-block:: c#

    using RazorEngine;
    using RazorEngine.Templating;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Net;
    using System.Net.Mail;
    using System.Threading.Tasks;
    using System.Web;

    namespace SendEmail.Core.Emails
    {
        /// <summary>
        /// Envía un simple email usando templates Razor.
        /// Se puede enviar el email en texto plano o HTML.
        ///
        /// Los templates deben estar (por defecto) en el directorio ~/Views/TemplateEmails
        /// y pasar el nombre y la extension "MiTemplate.cshtml|txt".
        ///
        /// Si no se va a usar ViewModel, usar <object> en el genérico.
        ///
        /// Example:
        ///
        /// -> Instanciando:
        /// ========================================================
        ///
        /// SimpleEmail<Person> email = new SimpleEmail<Person>
        /// {
        ///     Template = "Register.html",
        ///     Subject = "Email de prueba",
        ///     From = new MailAddress("perico@example.com"),
        ///     To = new List<MailAddress>
        ///     {
        ///         new MailAddress("palote@example.com")
        ///     },
        ///     ViewModel = model // Opcional, en el genérico poner SimpleEmail<object> si no se añade model.
        /// };
        /// email.SendAsHtml();
        /// await email.SendAsHtmlAsync();
        /// email.SendAsText();
        /// await email.SendAsTextAsync();
        ///
        /// -> Static
        /// ========================================================
        ///
        /// await SimpleEmail<Persona>.SendAsync|SimpleEmail<Persona>.Send(
        ///     "Register.cshtml",
        ///     "Email de prueba",
        ///      new MailAddress("snicoper@ofervivienda.com"),
        ///      new List<MailAddress>
        ///      {
        ///         new MailAddress("snicoper@gmail.com")
        ///      },
        ///      model // Opcional, en el genérico poner SimpleEmail<object> si no se añade model.
        ///      true // Opcional, por defecto true.
        /// );
        ///
        /// Required:
        ///
        /// Install-Package RazorEngine // https://antaris.github.io/RazorEngine/
        ///
        /// En Web.config (de la raíz) requiere añadir en appSettings:
        ///
        /// <!-- SMTP -->
        /// <add key="SMTPHost" value="smtp.example.com" />
        /// <add key="SMTPEnableSsl" value="true"/>
        /// <add key="SMTPUserName" value="username@example.com" />
        /// <add key="SMTPPassword" value="mi_password" />
        /// <add key="SMTPPort" value="587" />
        /// <!-- End SMTP -->
        ///
        /// Limitaciones:
        /// No tiene implementado CC, BCC, ReplyTo entre otras.
        /// </summary>
        public class SimpleEmail<TModel> : IDisposable
        {
            /// <summary>
            /// Template para el email.
            /// </summary>
            public string Template { get; set; }

            /// <summary>
            /// Titulo del email.
            /// </summary>
            public string Subject { get; set; }

            /// <summary>
            /// Cabecera FROM:
            /// </summary>
            public MailAddress From { get; set; }

            /// <summary>
            /// Lista de emails destinatarios.
            /// </summary>
            public List<MailAddress> To { get; set; }

            /// <summary>
            /// Keys => Values para remplazarlo en Template.
            /// </summary>
            public TModel ViewModel { get; set; }

            /// <summary>
            /// ¿El email sera enviado como HTML?
            /// </summary>
            private bool _isBodyHtml { get; set; }

            /// <summary>
            /// Cuerpo del email.
            /// </summary>
            private string _body { get; set; }

            // SMTP
            private MailMessage _mailMessage;
            private NetworkCredential _networkCredential;
            private SmtpClient _smtpClient;

            /// <summary>
            /// Directorio contenedor de los templates.
            /// Ha de ser un ruta relativa desde el root del proyecto.
            /// Utiliza Server.MapPath para componer la ruta absoluta.
            /// No añadir / al final.
            /// </summary>
            private const string TEMPLATE_DIR = "~/Views/TemplateEmails";

            public SimpleEmail()
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
            /// Envía un email asíncrono con template como HTML.
            /// </summary>
            public async Task SendAsHtmlAsync()
            {
                _isBodyHtml = true;
                _body = _render();
                await _sendAsync();
            }

            /// <summary>
            /// Envía un email con template como HTML.
            /// </summary>
            public void SendAsHtml()
            {
                _isBodyHtml = true;
                _body = _render();
                _send();
            }

            /// <summary>
            /// Envía un email asíncrono con template como texto plano.
            /// </summary>
            public async Task SendAsTextAsync()
            {
                _isBodyHtml = false;
                _body = _render().Replace(Environment.NewLine, "\n");
                await _sendAsync();
            }

            /// <summary>
            /// Envía un email con template como texto plano.
            /// </summary>
            public void SendAsText()
            {
                _isBodyHtml = false;
                _body = _render().Replace(Environment.NewLine, "\n");
                _send();
            }

            /// <summary>
            /// Envía un email asíncrono.
            /// </summary>
            /// <typeparam name="T">Model View para la vista</typeparam>
            /// <param name="template">Nombre del archivo View, con la extensión</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">De</param>
            /// <param name="to">Para</param>
            /// <param name="viewModel">Modelo para Razor en la View</param>
            /// <param name="asHtml">¿Mandar email como HTML?</param>
            /// <returns></returns>
            public static async Task SendAsync<T>(string template, string subject, MailAddress from, List<MailAddress> to, T viewModel, bool asHtml = true)
            {
                SimpleEmail<T> email = _getInstance(template, subject, from, to, viewModel);
                if (asHtml)
                {
                    await email.SendAsHtmlAsync();
                }
                else
                {
                    await email.SendAsTextAsync();
                }
            }

            /// <summary>
            /// Envía un email.
            /// </summary>
            /// <typeparam name="T">Model View para la vista</typeparam>
            /// <param name="template">Nombre del archivo View, con la extensión</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">De</param>
            /// <param name="to">Para</param>
            /// <param name="viewModel">Modelo para Razor en la View</param>
            /// <param name="asHtml">¿Mandar email como HTML?</param>
            /// <returns></returns>
            public static void Send<T>(string template, string subject, MailAddress from, List<MailAddress> to, T viewModel, bool asHtml = true)
            {
                SimpleEmail<T> email = _getInstance(template, subject, from, to, viewModel);
                if (asHtml)
                {
                    email.SendAsHtml();
                }
                else
                {
                    email.SendAsText();
                }
            }

            /// <summary>
            /// Envía el email asíncrono.
            /// </summary>
            private async Task _sendAsync()
            {
                _prepare();
                await _smtpClient.SendMailAsync(_mailMessage);
            }

            /// <summary>
            /// Envía el email.
            /// </summary>
            private void _send()
            {
                _prepare();
                _smtpClient.Send(_mailMessage);
            }

            /// <summary>
            /// Obtener instance de SimpleEmail con método estático para enviar un email.
            /// </summary>
            /// <typeparam name="T"></typeparam>
            /// <param name="template">Nombre del archivo View, con la extensión</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">De</param>
            /// <param name="to">Para</param>
            /// <param name="viewModel">Modelo para Razor en la View</param>
            /// <returns></returns>
            private static SimpleEmail<T> _getInstance<T>(string template, string subject, MailAddress from, List<MailAddress> to, T viewModel)
            {
                SimpleEmail<T> email = new SimpleEmail<T>
                {
                    Template = template,
                    Subject = subject,
                    From = from,
                    To = to,
                    ViewModel = viewModel
                };
                return email;
            }

            /// <summary>
            /// Puebla los campos requeridos de EmailMessage.
            /// </summary>
            private void _prepare()
            {
                _mailMessage.From = From;
                _mailMessage.Subject = Subject;
                _mailMessage.Body = _body;
                _mailMessage.IsBodyHtml = _isBodyHtml;

                foreach (var m in To)
                {
                    _mailMessage.To.Add(m);
                }
            }

            /// <summary>
            /// Obtiene un template y remplaza el contexto.
            /// Si el template no existe, lanzara FileNotFoundException.
            /// </summary>
            private string _render()
            {
                string result;

                if (Template == string.Empty)
                {
                    string message = "La propiedad \"Template\" no contiene valor y es requerido";
                    throw new SettingsPropertyNotFoundException(message);
                }

                // Obtener el template y pasarlo a string.
                string template = HttpContext.Current.Server.MapPath($"{TEMPLATE_DIR}/{Template}");

                // Lanza un FileNotFoundException si el archivo no existe.
                if (!File.Exists(template))
                {
                    string filename = Path.GetFileName(template);
                    string message = $"El archivo {filename} no existe en {template}";
                    throw new FileNotFoundException(message);
                }

                string content = File.ReadAllText(template);

                // Solo si Model tiene "contexto", usa Razor engine.
                if (ViewModel != null)
                {
                    result = Engine.Razor.RunCompile(content, Template, null, ViewModel);
                }
                else
                {
                    result = content;
                }
                return result;
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
        <add key="SMTPHost" value="smtp.gmail.com"/>
        <add key="SMTPEnableSsl" value="true"/>
        <add key="SMTPUserName" value="username@gmail.com"/>
        <add key="SMTPPassword" value="MI_PASSWORD"/>
        <add key="SMTPPort" value="587" />
    </appSettings>
