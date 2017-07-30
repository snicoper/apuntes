.. _reference-programacion-asp_mvc-connectionstring:

################
connectionString
################

Usando **LocalDb** en el directorio ``App_Data``

.. code-block:: xml

    <add name="ApplicationDbContext"
         connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDb Filename=|DataDirectory|\NOMBRE_PROYECTO.mdf;Initial Catalog=NOMBRE_PROYECTO;Integrated Security=True"
         providerName="System.Data.SqlClient" />
