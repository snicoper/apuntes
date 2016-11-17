.. _reference-linux-ubuntu-postfix:

#######
Postfix
#######

Instalación
***********

.. code-block:: bash

    sudo apt-get install postfix sasl2-bin dovecot-common dovecot-pop3d dovecot-imapd

Postfix
=======

* Durante la instalación cuando pregunte por el certificado SSL, decir que no.
* Después darle a ``<ok>``
* Por ultimo, ``No configuration``

.. code-block:: bash

    sudo cp /usr/lib/postfix/main.cf /etc/postfix/main.cf

.. code-block:: bash

    sudo vim /etc/postfix/main.cf

.. code-block:: bash

    # line 59: uncomment
    mail_owner = postfix

    # line 76: uncomment and specify hostname
    myhostname = mail.workspace.local

    # line 83: uncomment and specify domain name
    mydomain = workspace.local

    # line 104: uncomment
    myorigin = $mydomain

    # line 118: uncomment
    inet_interfaces = all

    # line 166: uncomment
    mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

    # line 209: uncomment
    local_recipient_maps = unix:passwd.byname $alias_maps

    # line 268: uncomment and specify your LAN
    mynetworks = 192.168.0.0/24, 127.0.0.0/16

    # line 388: uncomment
    alias_maps = hash:/etc/aliases

    # line 399: uncomment
    alias_database = hash:/etc/aliases

    # line 421: uncomment (use Maildir)
    home_mailbox = Maildir/

    # line 531: uncomment
    header_checks = regexp:/etc/postfix/header_checks

    # add: mail body checking
    body_checks = regexp:/etc/postfix/body_checks

    # line 557: make it comment and add below
    # smtpd_banner = $myhostname ESMTP $mail_name (@@DISTRO@@)
    smtpd_banner = $myhostname ESMTP

    # line 631: add
    sendmail_path = /usr/sbin/postfix

    # line 636: add
    newaliases_path = /usr/bin/newaliases

    # line 641: add
    mailq_path = /usr/bin/mail

    # line 647: add
    setgid_group = postdrop

    # line 651: make it comment
    # html_directory =

    # line 655: make it comment
    # manpage_directory =

    # line 660: make it comment
    # sample_directory

    # line 664: make it comment
    # readme_directory =

    # add at the lasdt line:
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
    smtpd_client_restrictions = permit_mynetworks,reject_unknown_client,permit
    smtpd_recipient_restrictions = permit_mynetworks,permit_auth_destination,permit_sasl_authenticated,reject

.. code-block:: bash

    sudo vim /etc/postfix/header_checks

.. code-block:: bash

    # add at the head ( reject if email address is empty )
    /^From:.*<#.*@.*>/ REJECT
    /^Return-Path:.*<#.*@.*>/ REJECT

.. code-block:: bash

    sudo vim /etc/postfix/body_checks

.. code-block:: bash

    # reject if includes 'example.com' in mail body
    /^(|[^>].*)example.com/ REJECT

.. code-block:: bash

    sudo vim /etc/aliases

    # Añadir
    root:   snicoper@mail.workspace.local

.. code-block:: bash

    sudo newaliases
    sudo service postfix restart

Dovecot
=======

.. code-block:: bash

    sudo vim /etc/dovecot/conf.d/10-auth.conf

.. code-block:: bash

    # line 10: uncomment and change ( allow plain text auth )
    disable_plaintext_auth = no

    # line 100: add
    auth_mechanisms = plain login

.. code-block:: bash

    sudo vim /etc/dovecot/conf.d/10-mail.conf

.. code-block:: bash

    # line 30: uncomment and add
    mail_location = maildir:~/Maildir

.. code-block:: bash

    sudo vim /etc/dovecot/conf.d/10-master.conf

.. code-block:: bash

    # line 95: uncomment and add
    # Postfix smtp-auth
        unix_listener /var/spool/postfix/private/auth {
        mode = 0666
        user = postfix # add
        group = postfix # add
    }

.. code-block:: bash

    sudo service dovecot restart

SSL
===

Ver :ref:`reference-linux-ubuntu-crear_certificado_ssl`

.. code-block:: bash

    sudo vim /etc/postfix/main.cf

.. note::
    Usar ``lxmaq1.crt`` y ``lxmaq1.key`` con los mismos nombres que se hayan
    creado en :ref:`reference-linux-ubuntu-crear_certificado_ssl`

.. code-block:: bash

    # add at the last line
    # SSL
    smtpd_use_tls = yes
    smtpd_tls_cert_file = /etc/ssl/private/lxmaq1.crt
    smtpd_tls_key_file = /etc/ssl/private/lxmaq1.key
    smtpd_tls_session_cache_database = btree:${data_directory}/smtpd_scache

.. code-block:: bash

    sudo vim /etc/postfix/master.cf

.. code-block:: bash

    # line 28-30: uncomment
    smtps     inet  n       -       -       -       -       smtpd
      -o syslog_name=postfix/smtps
      -o smtpd_tls_wrappermode=yes

.. code-block:: bash

    sudo vim /etc/dovecot/conf.d/10-ssl.conf

.. code-block:: bash

    # line 6: uncomment
    ssl = yes

    # line 12,13: uncomment and specify certificate
    ssl_cert = </etc/ssl/private/lxmaq1.crt
    ssl_key = </etc/ssl/private/lxmaq1.key

.. code-block:: bash

    sudo service postfix restart
    sudo service dovecot restart
