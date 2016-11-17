.. _reference-programacion-csharp-csharp_script-envio_email_smtp_csharp:

##########################
Envío Email usando SMTP C#
##########################

.. code-block:: c#

    using System.Net.Mail;

    /// <summary>
    /// Enviar un email
    /// </summary>
    /// <returns>true en caso de éxito, false en caso contrario.</returns>
    public bool Send()
    {
        try
        {
            MailMessage mail = new MailMessage();
            mail.IsBodyHtml = true;
            mail.From = new MailAddress("snicoper@gmail.com", "snicoper");
            mail.To.Add(new MailAddress("snicoper@outlook.com", "Salvador Nicolas"));
            mail.Subject = "Mensaje de prueba desde C# .NET";
            mail.Body = "<h1>Mensaje de prueba!!<h1>";

            using (SmtpClient smtp = new SmtpClient())
            {
                smtp.Host = "smtp.gmail.com";
                smtp.Port = 587;
                smtp.EnableSsl = true;
                System.Net.NetworkCredential NetworkCred = new System.Net.NetworkCredential();
                NetworkCred.UserName = "snicoper@gmail.com";
                NetworkCred.Password = "123456";
                smtp.UseDefaultCredentials = true;
                smtp.Credentials = NetworkCred;
                smtp.Send(mail);
            }
        }
        catch (Exception)
        {
            return false;
        }

        return true;
    }

.. note::
    También puede interesar.

    * https://github.com/jstedfast/MailKit
    * https://github.com/jstedfast/MimeKit
