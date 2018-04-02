.. _reference--windows-sqlexpress_conection_ip:

############################
Conectar a SQLExpress por ip
############################

**Fuentes**

* https://dba.stackexchange.com/a/62300

---

* Abrir ``SQL Server Network Configuration > Protocols for SQLEXPRESS``
* Doble click ``TCP/IP``
* Seleccionar ``Yes`` en la opción ``Enabled``
* Seleccionar la pestaña ``IP Addresses``
* En la sección ``IPALL`` la opción ``TCP Port`` poner ``1433`` (Si TCP Dynamic Ports tiene algún valor, quitarlo)
* Añadir puerto en el firewall de windows, tanto en ``Inbound Rules`` como en ``Outbound Rules``
