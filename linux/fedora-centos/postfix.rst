.. _reference-linux-fedora-centos-postfix:

#######
Postfix
#######

.. note::
    Probado en Fedora 30, Centos 7
-------------------

Servidor postfix
****************

Instalación de postfix.

.. code-block:: bash

    dnf install -y postfix dovecot

Editar archivo de configuración.

.. code-block:: bash

    vim /etc/postfix/main.cf

.. code-block:: bash

    # line 94 (75): uncomment and specify hostname
    myhostname = mail.snicoper.local

    # line 102 (83): uncomment and specify domain name
    mydomain = snicoper.local

    # line 118 (99): uncomment
    myorigin = $mydomain

    # line 132 (113): uncomment
    inet_interfaces = all

    # line 135 (116): comment
    # inet_interfaces = localhost

    # line 183 (164): comentar
    #mydestination = $myhostname, localhost.$mydomain, localhost

    # line 184 (165): descomentar
    mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

    # line 283 (264): uncomment and specify your LAN
    mynetworks = 192.168.1.0/24, 127.0.0.0/8

    # line 438 (419): uncomment (use Maildir)
    home_mailbox = Maildir/

    # line 593 (574): add
    smtpd_banner = $myhostname ESMTP

    # add at the last line

    # limit an email size 10M
    message_size_limit = 10485760

    # limit mailbox 1G
    mailbox_size_limit = 1073741824

    # for SMTP-Auth settings
    smtpd_sasl_type = dovecot
    smtpd_sasl_path = private/auth
    smtpd_sasl_auth_enable = yes
    smtpd_sasl_security_options = noanonymous
    smtpd_sasl_local_domain = $myhostname

    # http://serverfault.com/questions/775415/postfix-noqueue-reject-rcpt-from-unknown
    #smtpd_client_restrictions = permit_mynetworks,reject_unknown_client,permit
    #smtpd_recipient_restrictions = permit_mynetworks,permit_auth_destination,permit_sasl_authenticated,reject
    smtpd_recipient_restrictions = permit_sasl_authenticated, reject_unauth_destination
    smtpd_sender_restrictions = reject_unknown_sender_domain

Dovecot
*******

.. code-block:: bash

    vim /etc/dovecot/dovecot.conf

.. code-block:: bash

    # line 24: uncomment
    protocols = imap pop3 lmtp submission

.. code-block:: bash

    vim /etc/dovecot/conf.d/10-auth.conf

.. code-block:: bash

    # line 10: uncomment and change ( allow plain text auth )
    disable_plaintext_auth = no

.. code-block:: bash

    # line 100: add 'login'
    auth_mechanisms = plain login

.. code-block:: bash

    vim /etc/dovecot/conf.d/10-mail.conf

.. code-block:: bash

    # line 30: uncomment and add
    mail_location = maildir:~/Maildir

.. code-block:: bash

    vim /etc/dovecot/conf.d/10-master.conf

.. code-block:: bash

    # line 107: uncomment and add

    # Postfix smtp-auth
    unix_listener /var/spool/postfix/private/auth {
        mode = 0666
        user = postfix # add
        group = postfix # add
    }

.. code-block:: bash

    vim /etc/aliases

.. code-block:: bash

    # En la ultima linea agregar
    root: snicoper

.. code-block:: bash

    postalias /etc/aliases
    newaliases

.. important::
    | Ver :ref:`reference-linux-fedora-centos-reglas_selinux`
    | Para crear el certificado SSL, :ref:`reference-linux-fedora-centos-crear_ssl`

.. code-block:: bash

    vim /etc/postfix/main.cf

.. code-block:: bash

    # add at the last line
    # SSL
    smtpd_use_tls = yes
    smtpd_tls_cert_file = /etc/pki/tls/certs/snicoper.crt
    smtpd_tls_key_file = /etc/pki/tls/certs/snicoper.key
    smtpd_tls_session_cache_database = btree:/etc/postfix/smtpd_scache
    # Centos 7
    #smtpd_tls_session_cache_database = btree:/var/lib/postfix/smtpd_scache

.. code-block:: bash

    vim /etc/postfix/master.cf

.. code-block:: bash

    # Descomentar linea 29 (26)
    smtps       inet   n       -       n       -       -       smtpd

    # Descomentar lineas 30 (27) y 31 (28)
    -o syslog_name=postfix/smtps
    -o smtpd_tls_wrappermode=yes

.. code-block:: bash

    vim /etc/dovecot/conf.d/10-ssl.conf

.. code-block:: bash

    # line 8: uncomment
    ssl = yes

    # line 14,15: comentar
    # line 16: añadir and specify certificate
    ssl_cert = </etc/pki/tls/certs/snicoper.crt
    ssl_key = </etc/pki/tls/certs/snicoper.key

.. code-block:: bash

    systemctl start postfix.service
    systemctl enable postfix.service
    systemctl start dovecot.service
    systemctl enable dovecot.service

Poner por defecto (si no lo esta) ``postfix``

.. code-block:: bash

    alternatives --config mta

Firewall
********

.. code-block:: bash

    firewall-cmd --permanent --zone=public --add-service=smtp
    firewall-cmd --reload

Lista de puertos por defecto
============================

.. code-block:: bash

    POP3 - port 110
    IMAP - port 143
    SMTP - port 25
    HTTP - port 80
    Secure SMTP (SSMTP) - port 465
    Secure IMAP (IMAP4-SSL) - port 585
    IMAP4 over SSL (IMAPS) - port 993
    Secure POP3 (SSL-POP) - port 995
