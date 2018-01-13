.. _reference-programacion-csharp-dotnet_core-generar_slug:

############
Generar Slug
############

Para generar un slug, como ejemplo un ``Article``

.. code-block:: csharp

    public class Article
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Slug { get; set; }
    }

Crear una clase de **extension** de **string**

.. code-block:: csharp

    public static class Text
    {
        public static string Slugify(this string text)
        {
            var pattern = @"[^a-zA-Z0-9\-]";
            var replacement = "-";
            var regex = new Regex(pattern);
            var result = regex.Replace(RemoveDiacritics(text), replacement).Replace("--", "-").Trim('-');
            return result;
        }

        private static string RemoveDiacritics(string text)
        {
            var normalizedString = text.ToLower().Trim().Normalize(NormalizationForm.FormD);
            var stringBuilder = new StringBuilder();
            foreach (var c in normalizedString)
            {
                var unicodeCategory = CharUnicodeInfo.GetUnicodeCategory(c);
                if (unicodeCategory != UnicodeCategory.NonSpacingMark)
                {
                    stringBuilder.Append(c);
                }
            }
            return stringBuilder.ToString().Normalize(NormalizationForm.FormC);
        }
    }

Antes de guardar el **Article**, generar un ``Slug``

.. code-block:: csharp

    public void Create(Article model)
    {
        model.Slug = model.Title.Slugify();
        _context.Articles.Add(model);
        _context.SaveChanges();
    }
