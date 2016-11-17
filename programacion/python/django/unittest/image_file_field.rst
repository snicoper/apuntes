====================
ImageField FileField
====================

En primer en el directorio donde tengo los ``test_xxx.py`` pongo una imagen que sirva para las
pruebas.

Pongo en algún sitio de los test (compartido) ``images.py`` y dentro:

.. code-block:: python

    from django.core.files.uploadedfile import SimpleUploadedFile

    def simple_uploaded_file(image_path):
    """Crea una SimpleUploadedFile para campos de modelo
    ImageField, FileField.

    Args:
        image_path (str): Path de la imagen a "subir".

    Returns:
        SimpleUploadedFile:
    """
    if not os.path.exists(image_path):
        raise FileNotFoundError('El "{}" archivo no existe'.format(image_path))
    name = os.path.basename(image_path)
    with open(image_path, 'rb') as fh:
        image = SimpleUploadedFile(
            name=name,
            content=fh.read(),
            content_type='image/jpeg'
        )
    return image

Ahora, en el inicio del archivo (antes de cualquier clase):

.. code-block:: python

    image_path = os.path.join(os.path.dirname(__file__), 'image_test.jpg')

Y ahora, dentro del una clase test, en ``setUp``

.. code-block:: python

    def setUp(self):
        super().setUp()
        self.image = simple_uploaded_file(image_path)

Hay que procurar eliminar siempre la imagen.
