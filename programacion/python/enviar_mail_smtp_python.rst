.. _reference-programacion-python-enviar_mail_smtp_python:

#################
Enviar email SMTP
#################

Fuentes
*******

* http://www.mkyong.com/python/how-do-send-email-in-python-via-smtplib/
* http://docs.python.org/3.3/library/smtplib.html

----------

.. code-block:: python

    import smtplib

    to = 'mkyong2002@yahoo.com'
    gmail_user = 'mkyong2002@gmail.com'
    gmail_pwd = 'yourpassword'
    smtpserver = smtplib.SMTP("smtp.gmail.com", 587)
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo
    smtpserver.login(gmail_user, gmail_pwd)
    header = 'To:' + to + '\n' + 'From: ' + gmail_user + '\n' + 'Subject:testing \n'
    print header
    msg = header + '\n this is test msg from mkyong.com \n\n'
    smtpserver.sendmail(gmail_user, to, msg)
    print 'done!'
    smtpserver.close()
