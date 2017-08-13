.. _reference-programacion-asp_mvc-connectionstring:

################
connectionString
################

LocalDB archivo en App_Data
===========================

.. code-block:: xml

    <add name="ApplicationDbContext"
         connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDb Filename=|DataDirectory|\NOMBRE_PROYECTO.mdf;Initial Catalog=NOMBRE_PROYECTO;Integrated Security=True"
         providerName="System.Data.SqlClient" />

Usando SQLEXPRESS
=================

.. code-block:: xml

    <add name="ApplicationDbContext"
         connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=NOMBREDB;Integrated Security=False;User Id=USUARIO;Password=PASSWORD;MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
