.. _reference-programacion-csharp-csharp_script-redimensaionar_imagen_csharp:

#######################
Redimensionar imagen C#
#######################

.. code-block:: c#

    using System.Drawing;
    using System.Drawing.Drawing2D;
    using System.IO;

    namespace HaveYouSeenMe.Models.Business
    {
        public class PetManagement
        {
            /// <summary>
            /// Redimensiona una imagen a un ancho/alto dado.
            /// </summary>
            /// <param name="filename">Nombre del archivo, incluida extension</param>
            /// <param name="filepath">directorio contenedor para guardar</param>
            /// <param name="thumbWi">Ancho de la imagen a redimensionar</param>
            /// <param name="thumbHi">Alto de la imagen a redimensionar</param>
            /// <param name="maintainAspect">Mantener proporciones ancho/alto?</param>
            public static void CreateThumbnail(string filename, string filepath,
                int thumbWi, int thumbHi, bool maintainAspect)
            {
                // Do nothing if the original is smaller than the designated
                // thumbnail dimensions
                var originalFile = Path.Combine(filepath, filename);
                var source = Image.FromFile(originalFile);

                if (source.Width <= thumbWi && source.Height <= thumbHi) return;

                Bitmap thumbnail;
                try
                {
                    int wi = thumbWi;
                    int hi = thumbHi;

                    if (maintainAspect)
                    {
                        // Maintain the aspect ratio despite the thumbnail size parameters
                        if (source.Width > source.Height)
                        {
                            wi = thumbWi;
                            hi = (int)(source.Height * ((decimal)thumbWi / source.Width));
                        }
                        else
                        {
                            hi = thumbHi;
                            wi = (int)(source.Width * ((decimal)thumbHi / source.Height));
                        }
                    }

                    thumbnail = new Bitmap(wi, hi);

                    using (Graphics g = Graphics.FromImage(thumbnail))
                    {
                        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
                        g.FillRectangle(Brushes.Transparent, 0, 0, wi, hi);
                        g.DrawImage(source, 0, 0, wi, hi);
                    }

                    var thumbnailName = Path.Combine(filepath, "thumbnail_" + filename);
                    thumbnail.Save(thumbnailName);
                }
                catch { }
            }
        }
    }
