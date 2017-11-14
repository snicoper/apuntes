.. _reference-linux-logrotate:

################################################
Logrotate, comprimir archivos log periódicamente
################################################

La herramienta **logrotate** está diseñada para simplificar la administración de los archivos de
registro en un sistema que genera una gran cantidad de archivos de registro. **Logrotate** permite
la rotación, compresión automática, eliminación y envío de archivos de registro por correo.
**Logrotate** se puede configurar para manejar un archivo de registro diario, semanal, mensual o
cuando el archivo de registro llega a cierto tamaño.

El archivo principal de **logrotate** se encuentra en ``/etc/logrotate.conf`` y el directorio donde
guarda las configuraciones de los diferentes programas que generan logs en ``/etc/logrotate.d/``.
Cada archivo es una configuración que se ejecuta dependiendo de las opciones que pongamos en el archivo.

Por ejemplo, para el ejemplo del otro día **"link eliminado"** genera un archivo de registro en
``~/webapps/examplecom/logs/gunicorn.log``, ese archivo, dependiendo del trafico del sitio, puede
llegar a ser muy grande y logrotate puede ayudarnos a partir ese archivo, comprimir y/o enviarlo por email.

Seguiré con el ejemplo de **gunicorn** y **nginx**, lo primero es crear un archivo de configuración
en ``/etc/logrotate.d/``.

.. code-block:: bash

    su
    vim /etc/logrotate.d/gunicorn

Y ponemos una simple configuración:

.. code-block:: bash

    /var/log/gunicorn/*log {
        create 0644 snicoper snicoper
        daily
        rotate 10
        missingok
        notifempty
        compress
    }

Acordaros de cambiar el **usuario/grupo**

Lo guardamos y probamos si funciona con el siguiente comando.

.. code-block:: bash

    logrotate -f /etc/logrotate.d/gunicorn

Si miráis en ``/var/log/gunicorn/`` veréis que hay un archivo ``.gz`` ``gunicorn.log.1.gz``, que es
el archivo log que había, lo ha comprimido y ha creado otro con el mismo nombre para seguir
insertando registros.

Aquí hay algunas opciones mas que se pueden poner **(sacado de man logrotate)**:

* **compress**: Las versiones antiguas de los archivos de registro se comprimen con gzip.
* **rotate**: Los  archivos  de registro se cambian <count> veces antes de ser eliminados o enviados a la dirección especificada en una directiva mail. Si count es 0, las versiones antiguas se eliminarán en vez de ser cambiadas.
* **daily**: Los archivos de registro se cambian diariamente.
* **notifempty**:No  rota  el  archivo  de  registro si está vacío (esto anula la opción ifempty).
* **create (mode owner group)**:  Se crea el archivo de registro (con el mismo nombre del  archivo de  registro  que  se acaba de rotar) inmediatamente después del cambio (antes de que se  ejecute  el  script  postrotate).  mode especifica  el  modo  del archivo de registro en octal (al igual que chmod (2)), owner especifica el nombre del  usuario  al  que pertenecerá  el archivo de registro, y group especifica el grupo al que pertenecerá el archivo. Se puede omitir cualquiera de los atributos  del  archivo  de  registro,  en  cuyo  caso, el nuevo archivo usará los valores  del  archivo  antiguo  para  aquellos atributos  que  se  hayan  omitido.  Esta opción se puede anular usando la opción nocreate.
* **postrotate/endscript**: Las líneas entre postrotate y endscript (ambas deben aparecer en líneas por separado) se ejecutan  una  vez  que  el  archivo  de registro  ha  sido rotado. Estas directivas sólo pueden aparecer dentro de una definición de archivo de registro.

----

**Fuentes**

* man logrotate
* http://manpages.ubuntu.com/manpages/lucid/es/man8/logrotate.8.html
* https://www.linode.com/docs/uptime/logs/use-logrotate-to-manage-log-files
* http://linuxconfig.org/logrotate
