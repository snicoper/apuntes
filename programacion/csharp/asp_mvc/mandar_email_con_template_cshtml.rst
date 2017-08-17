.. _reference-programacion-asp_mvc-mandar_email_con_template_cshtml:

#############################
Mandar Email con View .cshtml
#############################

Mandar un email con un template ``.cshtml`` o ``.txt``

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
        /// var viewModel = new Person { Username = "Perico de los Palotes", Email = "perico@example.com" }; // Opcional
        /// SimpleEmail.Send(template, subject, from, to, viewModel);
        ///
        /// Require:
        ///
        /// https://gist.github.com/HarveyWilliams/0405edd6719c16171329
        ///
        /// Web.config en appSettings
        ///
        /// <add key="SMTPDefaultFrom" value="default@example.com"/>
        /// <add key="SMTPHost" value="smtp.gmail.com"/>
        /// <add key="SMTPEnableSsl" value="true"/>
        /// <add key="SMTPUserName" value="user@gmail.com"/>
        /// <add key="SMTPPassword" value="PASSWORD"/>
        /// <add key="SMTPPort" value="587"/>
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
            /// ViewModel para la View.
            /// </summary>
            private object _viewModel;

            /// <summary>
            /// Directorio de Views.
            /// </summary>
            private const string TEMPLATE_DIR = "~/Views/TemplateEmails/";

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
            /// <param name="viewModel">ViewModel para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static async Task SendAsync(string template, string subject, MailAddress from, List<MailAddress> to, object viewModel = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, from, to, viewModel, isBodyHtml);
                await email._sendAsync();
            }

            /// <summary>
            /// Envía un email asíncrono.<br>
            /// El campo From: lo obtendrá de SMTPDefaultFrom del archivo de configuración.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="viewModel">ViewModel para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static async Task SendAsync(string template, string subject, List<MailAddress> to, object viewModel = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, null, to, viewModel, isBodyHtml);
                await email._sendAsync();
            }

            /// <summary>
            /// Envía un email.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="from">Cabeceras para From:</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="viewModel">ViewModel para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static void Send(string template, string subject, MailAddress from, List<MailAddress> to, object viewModel = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, from, to, viewModel, isBodyHtml);
                email._send();
            }

            /// <summary>
            /// Envía un email.<br>
            /// El campo From: lo obtendrá de SMTPDefaultFrom del archivo de configuración.
            /// </summary>
            /// <param name="template">Nombre del archivo en ~/Views/TemplateEmails/</param>
            /// <param name="subject">Titulo del mensaje</param>
            /// <param name="to">Lista de emails de recepción</param>
            /// <param name="viewModel">ViewModel para el contexto</param>
            /// <param name="isBodyHtml">¿Mandar mensaje como HTML?</param>
            public static void Send(string template, string subject, List<MailAddress> to, object viewModel = null, bool isBodyHtml = true)
            {
                SimpleEmail email = _getInstance(template, subject, null, to, viewModel, isBodyHtml);
                email._send();
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
            private static SimpleEmail _getInstance(string template, string subject, MailAddress from, List<MailAddress> to, object viewModel, bool isBodyHtml)
            {
                from = from ?? new MailAddress(ConfigurationManager.AppSettings["SMTPDefaultFrom"]);

                SimpleEmail email = new SimpleEmail
                {
                    _template = template,
                    _subject = subject,
                    _from = from,
                    _to = to,
                    _viewModel = viewModel
                };
                email._isBodyHtml = isBodyHtml;
                email._render();
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
            /// Envía un email asíncrono.
            /// </summary>
            /// <returns></returns>
            private async Task _sendAsync()
            {
                _initialize();
                await _smtpClient.SendMailAsync(_mailMessage);
            }

            /// <summary>
            /// Envía un email.
            /// </summary>
            private void _send()
            {
                _initialize();
                _smtpClient.Send(_mailMessage);
            }

            /// <summary>
            /// Renderiza el archivo con Razor.
            /// </summary>
            private string _render()
            {
                string templatepath = $"{TEMPLATE_DIR}{_template}";
                var ext = Path.GetExtension(templatepath);
                if (ext == null || !templatepath.Contains(".cshtml"))
                {
                    templatepath += ".cshtml";
                }
                else
                {
                    throw new Exception($"{_template} requiere de una extension .cshtml");
                }
                _body = ViewRenderer.RenderView(templatepath, _viewModel);
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
        <add key="SMTPHost" value="smtp.gmail.com"/>
        <add key="SMTPEnableSsl" value="true"/>
        <add key="SMTPUserName" value="username@gmail.com"/>
        <add key="SMTPPassword" value="MI_PASSWORD"/>
        <add key="SMTPPort" value="587" />
    </appSettings>
