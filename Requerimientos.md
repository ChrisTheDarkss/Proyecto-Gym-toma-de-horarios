# Guía de Requerimientos - Sistema de Gestión para Gimnasio (Base de Datos NoSQL)

# 1. Descripción del Cliente y Problema Principal

Contexto General: El gimnasio ha experimentado un crecimiento sostenido en su número de miembros, lo que ha llevado a que sus procesos manuales y su sistema de gestión actual sean insuficientes. La falta de una herramienta centralizada y eficiente está generando problemas con los sistemas, afectando la experiencia del cliente, la eficiencia del personal y la rentabilidad del negocio

# 2. Tipos de Usuarios y Perfiles con Permisos

## Administrador (Dueño)

**Permisos**:

* Gestión completa de usuarios (
    crear= Nombre, Usuario, Contraseña, Rut, 
    editar= Usuario, contraseña, 
    eliminar= Usuario)
* Administración de membresías y planes
* Gestión de trabajadores
* Estadisticas de la cantidad de usuarios por hora y dia 
* Configuración del sistema = Control de horarios, aforo 

## Trabajadores (Staff)

**Permisos**:

* Verificar estado de membresías
* Gestionar membresia clientes en el gimnasio
* Ver cpos de horarios y disponibilidad

## Clientes

**Permisos**:

* Registrarse en el sistema
* Agendar y des agendar horarios
* Ver su historial de ingresos
* Ver estado de su membresía

---
3. Definición del MVP (Minimum Viable Product)
MVP - Versión 1.0 (Incluye)
Funcionalidades Core:
Registro de usuarios con datos básicos .
Gestión de membresías (estados: activa, expirada, suspendida).
Agendamiento básico de horarios por piso.
Bloqueo/permiso de acceso desde aplicación.
Registro de entrada y salida
Características Técnicas:
Base de datos MongoDB (Nosql).
Aplicación web para administración.
Reddis(Cache) para mayor velocidad

# 4. Datos que se necesitan Guardar
* Datos de clientes(Nombre, Usuario, Contraseña, Rut)  
* Membresia (activa, expirada, suspendida)
* Hora agendada
* Registro de entrada y salida 

# 5. Reglas de negocio
* El desajendamiento de hora actualizara automaticamente el stock de horas disponibles.
* El agendamiento de hora solo se puede hacer con una hora de anticipación.
* El agendamiento de hora solo se puede utilizar si tiene una cuenta con membresia activa.
* Si ya paso la hora especifica o esta en la hora justa, no se puede des-agendar.
* No se podra agendar horas con anticipacion de mas de 2 meses 