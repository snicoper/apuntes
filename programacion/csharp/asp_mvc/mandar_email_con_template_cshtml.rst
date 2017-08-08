.. _reference-programacion-asp_mvc-mandar_email_con_template_cshtml:

#############################
Mandar Email con View .cshtml
#############################

Mandar un email con un template ``.cshtml`` o ``.txt``

.. code-block:: csharp

    using RazorEngine;
    using RazorEngine.Templating;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Net;
    using System.Net.Mail;
    using System.Web;

    namespace SendEmail.Core.Emails
    {
        /// <summary>
        /// Envía un simple email usando templates Razor.
        /// Se puede enviar el email en texto plano o HTML.
        ///
        /// Los templates deben estar en el directorio ~/Views/TemplateEmails y pasar el nombre
        /// y la extension "MiTemplate.cshtml|txt"
        ///
        /// Example:
        /// SimpleEmail<Person> email = new SimpleEmail<Person>
        /// {
        ///     Template = "Register.html",
        ///     Subject = "Email de prueba",
        ///     From = new MailAddress("perico@example.com"),
        ///     To = new List<MailAddress>
        ///     {
        ///         new MailAddress("palote@example.com")
        ///     },
        ///     Model = model
        /// };
        /// email.SendAsHtml();
        /// email.SendAsText();
        ///
        /// Required:
        ///
        /// Install-Package RazorEngine // https://antaris.github.io/RazorEngine/
        ///
        /// Requiere de los siguientes campos en Web.config de la raíz:
        ///
        /// <!-- SMTP -->
        /// <add key="Host" value="smtp.example.com" />
        /// <add key = "EnableSsl" value="true"/>
        /// <add key = "UserName" value="username@example.com" />
        /// <add key = "Password" value="mi_password" />
        /// <add key = "Port" value="587" />
        /// <!-- End SMTP -->
        ///
        /// Limitaciones:
        /// No tiene implementado CC, BCC, ReplyTo entre otras.
        /// </summary>
        public class SimpleEmail<TModel>
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
            /// Cuerpo del email, no requerido si se usa templates.
            /// </summary>
            public string Body { get; set; }

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
            public TModel Model { get; set; }

            private bool IsBodyHtml { get; set; }

            /// <summary>
            /// Envía un email con template como HTML.
            /// </summary>
            public void SendAsHtml()
            {
                IsBodyHtml = true;
                Body = _renderTemplate();
                _send();
            }

            /// <summary>
            /// Envía un email con template como texto plano.
            /// </summary>
            public void SendAsText()
            {
                IsBodyHtml = false;
                Body = _renderTemplate().Replace(Environment.NewLine, "\n");
                _send();
            }

            /// <summary>
            /// Se conecta al SMTP y envía el email.
            /// </summary>
            private void _send()
            {
                _checkProperties();

                using (var mail = new MailMessage())
                {
                    mail.From = From;
                    mail.Subject = Subject;
                    mail.Body = Body;
                    mail.IsBodyHtml = IsBodyHtml;

                    foreach (var m in To)
                    {
                        mail.To.Add(m);
                    }

                    var NetWorkCred = new NetworkCredential()
                    {
                        UserName = ConfigurationManager.AppSettings["UserName"],
                        Password = ConfigurationManager.AppSettings["Password"]
                    };

                    var smtp = new SmtpClient()
                    {
                        Host = ConfigurationManager.AppSettings["Host"],
                        EnableSsl = Convert.ToBoolean(ConfigurationManager.AppSettings["EnableSsl"]),
                        UseDefaultCredentials = true,
                        Credentials = NetWorkCred,
                        Port = int.Parse(ConfigurationManager.AppSettings["Port"])
                    };

                    smtp.Send(mail);
                }
            }

            /// <summary>
            /// Comprueba que todos los campos tienen valores.
            /// Estos son los campos requeridos en todos los SendAsXXX.
            /// </summary>
            private bool _checkProperties()
            {
                if (Template == string.Empty)
                {
                    _raiseException("Template");
                }
                if (Subject == string.Empty)
                {
                    _raiseException("Subject");
                }
                if (Body == string.Empty)
                {
                    _raiseException("Body");
                }
                if (From == null)
                {
                    _raiseException("From");
                }
                if (To.Count == 0)
                {
                    _raiseException("To");
                }
                return true;
            }

            /// <summary>
            /// Obtiene un template y remplaza el contexto.
            /// </summary>
            private string _renderTemplate()
            {
                // Obtener el template y pasarlo a string.
                HttpContext httpContext = HttpContext.Current;
                string template = httpContext.Server.MapPath($"~/Views/TemplateEmails/{Template}");

                // Lanza un FileNotFoundException si el archivo no existe.
                if (!File.Exists(template))
                {
                    string filename = Path.GetFileName(template);
                    string message = $"El archivo {filename} no existe en {template}";
                    throw new FileNotFoundException(message);
                }
                string content = File.ReadAllText(template);
                string result = Engine.Razor.RunCompile(content, Template, null, Model);
                return result;
            }

            /// <summary>
            /// Lanza SettingsPropertyNotFoundException si una propiedad requerida esta sin valor.
            /// </summary>
            /// <param name="fieldName">Nombre del campo</param>
            private void _raiseException(string fieldName)
            {
                string message = $"{fieldName} no contiene valor y es requerido";
                throw new SettingsPropertyNotFoundException(message);
            }
        }
    }


En el archivo ``Web.config``

.. code-block:: xml

    <appSettings>
        <!-- ... --->
        <add key="Host" value="smtp.gmail.com"/>
        <add key="EnableSsl" value="true"/>
        <add key="UserName" value="username@gmail.com"/>
        <add key="Password" value="MI_PASSWORD"/>
        <add key="Port" value="587" />
    </appSettings>
