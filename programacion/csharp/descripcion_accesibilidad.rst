.. _reference-programacion-csharp-descripcion_accesibilidad:

#########################
Descripción Accesibilidad
#########################

==============      =======================
Accessibility       Description
==============      =======================
public              No restrictions on access.
protected           Can be accessed in the declaring class or derived classes.
internal            Can be accessed by all types in the same assembly of the declaring class and other
assemblies          specifically named using the InternalsVisibleTo attribute.
protected           internal Any access granted by protected or internal.
private             Only accessed by the declaring class.
==============      =======================
