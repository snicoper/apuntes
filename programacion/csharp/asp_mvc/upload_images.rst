.. _reference-programacion-asp_mvc-upload_images:

##################################
Subir imágenes desde un formulario
##################################

El modelo

.. code-block:: csharp

    public class Usuario
    {
        # ...

        [StringLength(255)]
        public string PhotoPath { get; set; }

        [NotMapped]
        public HttpPostedFileBase File { get; set; }
    }


Desde el ``Controller`` (para abreviar), no comprueba si existe el directorio, ni nada,
solo es un recordatorio.

.. code-block:: csharp

    public string SaveImage([Bind(Include = "campos...")]Usuario usuario)
    {
        # ....

        var timestamp = DateTime.Now.ToString("ddMMyyyymmfffffff");
        var filename = String.Format("{0}-{1}", timestamp, Path.GetFileName(usuario.File.FileName));
        var filepath = Path.Combine(Server.MapPath("~/Content/Images/Usuarios"), filename);
        usuario.File.SaveAs(filepath);
        usuario.PhotoPath = filename;

        # ....
    }
