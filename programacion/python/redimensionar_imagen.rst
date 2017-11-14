####################
Redimensionar imagen
####################

.. code-block:: python

    import os
    from PIL import Image


    def resize_image(image_path, save_path, base_width, base_height, scale=True, prefix_name=None):
        """Redimensiona una imagen.

        Redimensiona una imagen a base_width y base_height, si scale es
        True, base_height redimensionara a escala de base_width.

        Si la base_width y base_height es mayor a la imagen original,
        dejara el tamaño original.

        args:
            image_path<str>: Path de la imagen a redimensionar.
            base_width<float|int>: Ancho máximo.
            base_height<float|int>: Alto máximo.
            scale<bool>: ¿Mantener proporción?.
            prefix_name<str>: Prefijo en el nombre de la imagen, no añadir el carácter '_'.
        raises:
            FileNotFoundError: Si no existe image_path.
        @return:
            void
        """
        if not os.path.exists(image_path):
            raise FileNotFoundError('La imagen {} no existe'.format(image_path))
        if prefix_name:
            basename = '{}_{}'.format(prefix_name, os.path.basename(save_path))
            dirname = os.path.dirname(save_path)
            save_path = os.path.join(dirname, basename)

        img = Image.open(image_path)
        img_width, img_height = float(img.size[0]), float(img.size[1])

        if img_width <= base_width and img_height <= base_height:
            img.save(save_path)
        else:
            width = base_width
            height = base_height
            if scale:
                if img_width > img_height or img_width == img_height:
                    width = base_width
                    height = int(img_height * (base_width / img_width))
                else:
                    height = base_height
                    width = int(img_width * (base_height / img_height))
            img = img.resize((width, height), Image.ANTIALIAS)
            img.save(save_path)
