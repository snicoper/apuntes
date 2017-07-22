.. _reference--windows-eliminar_ondedrive_del_explorer:

#############################
Eliminar OneDrive de Explorer
#############################

**Fuentes**

* https://www.tekrevue.com/tip/remove-onedrive-file-explorer-sidebar-windows-10/

--------------

Ejecutar ``regedit``

Buscar ``018D5C66-4533-4307-9B53-224DE2ED1FE6`` (``HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}``)

Modificar valor de ``System.IsPinnedToNameSpaceTree`` a ``0``