.. _reference-programacion-asp_mvc-ninject_mvc5:

##############################
Ninject proyecto ASP.NET MVC 5
##############################

**Fuentes**

* Pro ASP.NET MVC 5 de Apress

---

Añadir Ninject a un proyecto ASP.NET MVC 5.

Instalación
===========

.. code-block:: bash

    Install-Package Ninject
    Install-Package Ninject.Web.Common
    Install-Package Ninject.MVC5

Configuración
=============

Crear directorio ``Infrastructure`` y crear archivo (**class**) ``NinjectDependencyResolver.cs``

Añadir:

.. code-block:: csharp

    using Ninject;
    using System;
    using System.Collections.Generic;
    using System.Web.Mvc;

    namespace Practica.Infrastructure
    {
        public class NinjectDependencyResolver : IDependencyResolver
        {
            private IKernel _kernel;

            public NinjectDependencyResolver(IKernel kernel)
            {
                _kernel = kernel;
                AddBindings();
            }

            public object GetService(Type serviceType)
            {
                return _kernel.TryGet(serviceType);
            }

            public IEnumerable<object> GetServices(Type serviceType)
            {
                return _kernel.GetAll(serviceType);
            }

            private void AddBindings()
            {
                // Añadir los binds aquí.
                _kernel.Bind<IMiInterface>().To(MiClaseDerivada)();
            }
        }
    }

Registrar el Dependency Resolver
================================

Abrir ``App_Start/NinjectWebCommon.cs`` y en el metodo ``RegisterServices``, añadir:

.. code-block:: csharp

    private static void RegisterServices(IKernel kernel)
    {
        System.Web.Mvc.DependencyResolver.SetResolver(
            new Practica.Infrastructure.NinjectDependencyResolver(kernel)
        );
    }
