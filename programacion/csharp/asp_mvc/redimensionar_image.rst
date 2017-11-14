.. _reference-programacion-asp_mvc-redimensionar_image:

###########################
Redimensionar Imagen en MVC
###########################

**References**

* Libro ASP.NET MVC with Entity Framework and CSS (Chapter 5)

-----------

.. code-block:: csharp

    namespace BabyStore
    {
        public static class Constants
        {
            public const string ProductImagePath = "~/Content/ProductImages/";
            public const string ProductThumbnailPath = "~/Content/ProductImages/Thumbnails/";
        }
    }

.. code-block:: csharp

    namespace BabyStore.Controllers
    {
        public class ProductImagesController : Controller
        {
            public ActionResult Upload()
            {
                return View();
            }

            [HttpPost]
            [ValidateAntiForgeryToken]
            public ActionResult Upload(HttpPostedFileBase file)
            {
                if (file != null)
                {
                    if (ValidateFile(file))
                    {
                        try
                        {
                            SaveFileToDisk(file);
                        }
                        catch (Exception)
                        {
                            ModelState.AddModelError(
                                "FileName",
                                "Sorry an error occurred saving the file to disk, please try again"
                            );
                        }
                    }
                    else
                    {
                        ModelState.AddModelError(
                            "FileName",
                            "The file must be gift, png, pjeg or jpg and less than 2MB in size"
                        );
                    }
                }
                else
                {
                    ModelState.AddModelError("FileName", "Please choose a file");
                }
                if (ModelState.IsValid)
                {
                    db.ProductImages.Add(new ProductImage { FileName = file.FileName });
                }
                return View();
            }

            private bool ValidateFile(HttpPostedFileBase file)
            {
                string fileExtension = System.IO.Path.GetExtension(file.FileName).ToLower();
                string[] allowedFileTypes = { ".gif", ".png", ".jpeg", ".jpj" };
                if ((file.ContentLength > 0 && file.ContentLength < 2097152) && allowedFileTypes.Contains(fileExtension))
                {
                    return true;
                }
                return false;
            }

            private void SaveFileToDisk(HttpPostedFileBase file)
            {
                WebImage img = new WebImage(file.InputStream);
                if (img.Width > 190)
                {
                    img.Resize(190, img.Height);
                }
                img.Save(Constants.ProductImagePath + file.FileName);
                if (img.Width > 100)
                {
                    img.Resize(100, img.Height);
                }
                img.Save(Constants.ProductThumbnailPath + file.FileName);
            }
        }
    }
