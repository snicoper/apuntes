.. _reference-programacion-asp_mvc-mandar_email_con_template_cshtml:

#############################
Mandar Email con View .cshtml
#############################

.. warning:: No esta terminado, me lo dejo como apunte

Mandar un email con un template ``.cshtml``

.. code-block:: csharp

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Net;
    using System.Net.Mail;
    using System.Web.Mvc;

    namespace PartyInvites.Utils
    {
        public class EmailHtml
        {
            public string Template { get; set; }
            public Controller Controller { get; set; }
            public object Context { get; set; }

            public MailAddress From { get; set; }
            public List<MailAddress> To { get; set; }
            public string Subject { get; set; }
            protected string _body = string.Empty;

            protected string _renderRazorViewToString()
            {
                Controller.ViewData.Model = Context;

                using (var sw = new StringWriter())
                {
                    var viewResult = ViewEngines.Engines.FindPartialView(Controller.ControllerContext, Template);
                    var viewContext = new ViewContext(Controller.ControllerContext, viewResult.View, Controller.ViewData, Controller.TempData, sw);
                    viewResult.View.Render(viewContext, sw);
                    viewResult.ViewEngine.ReleaseView(Controller.ControllerContext, viewResult.View);
                    return sw.GetStringBuilder().ToString();
                }
            }

            public void Send()
            {
                _body = _renderRazorViewToString();

                using (var mailMessage = new MailMessage())
                {
                    mailMessage.From = From;
                    mailMessage.Subject = Subject;
                    mailMessage.Body = _body;
                    mailMessage.IsBodyHtml = true;

                    foreach (var m in To)
                    {
                        mailMessage.To.Add(m);
                    }

                    var NetWorkCred = new NetworkCredential()
                    {
                        UserName = ConfigurationManager.AppSettings["Username"],
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

                    smtp.Send(mailMessage);
                }
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

**Ejemplo:**

.. code-block:: csharp

    public class HomeController : Controller
    {
        [HttpPost]
        public ViewResult Success(FormResponse formResponse)
        {
            if (ModelState.IsValid)
            {
                var mail = new EmailHtml()
                {
                    Template = "~/Views/Emails/Hello.cshtml",
                    Controller = this,
                    Context = formResponse,
                    From = new MailAddress("snicoper@gmail.com"),
                    To = new List<MailAddress>
                    {
                        new MailAddress(formResponse.Email)
                    },
                    Subject = "Mensaje de prueba"
                };
                mail.Send();

                return View("Thanks", formResponse);
            }
            else
            {
                // there is a validation error
                return View();
            }
        }
    }

Crear la **View** ``~/Views/Emails/Hello2.cshtml``