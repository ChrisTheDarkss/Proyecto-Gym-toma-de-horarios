# Guía de Requerimientos - Sistema de Gestión para Gimnasio (Base de Datos NoSQL)

# 1. Descripción del Cliente y Problema Principal

Contexto General: El gimnasio ha experimentado un crecimiento sostenido en su número de miembros, lo que ha llevado a que sus procesos manuales y su sistema de gestión actual sean insuficientes. La falta de una herramienta centralizada y eficiente está generando problemas con los sistemas, afectando la experiencia del cliente, la eficiencia del personal y la rentabilidad del negocio.
## Problema Principal: Sistema ineficiente que genera:

* Mala gestión de usuarios y membresías.
* Problemas con control de horarios y aforo.
* Poca administración y seguimiento de ingresos.
* Falta de control en el acceso al establecimiento.

# 2. Tipos de Usuarios y Perfiles con Permisos

## Administrador (Dueño)

**Permisos**:

* Gestión completa de usuarios:

    Crear --> Nombre, Usuario, Contraseña, RUT. 

    Editar --> Usuario, contraseña. 
    
    Eliminar --> Usuario.
* Administración de membresías y planes.
* Gestión de trabajadores.
* Estadísticas de la cantidad de usuarios por hora y día. 
* Configuración del sistema: Control de horarios, aforo. 

## Trabajadores (Staff)

**Permisos**

* Verificar estado de membresías.
* Gestiónar membresía clientes en el gimnasio.
* Ver cupos de horarios y disponibilidad.

## Clientes

**Permisos**

* Registrarse en el sistema.
* Agendar y des agendar horarios.
* Ver su historial de ingresos.
* Ver estado de su membresía.

# 3. Definición del MVP (Minimum Viable Product)

## MVP - Versión 1.0 (Incluye)

### Funcionalidades Core:

* Registro de usuarios con datos básicos.
* Gestión de membresías (estados: activa, expirada, suspendida).
* Agendamiento básico de horarios por piso.
* Bloqueo/permiso de acceso desde aplicación.
* Registro de entrada y salida. 

### Características Técnicas:

* Base de datos MongoDB (NoSQL).
* Aplicación web para administración.
* Redis(Caché) para mayor velocidad. 

# 4. Datos que se necesitan Guardar
* Datos de clientes(Nombre, Usuario, Contraseña, RUT).  
* Membresía (activa, expirada, suspendida).
* Hora agendada.
* Registro de entrada y salida. 

# 5. Reglas de negocio
* La cancelacion de una hora actualizará
automáticamente el stock de horas disponibles.
* El agendamiento de hora solo se puede hacer con una hora de anticipación.
* El agendamiento de hora solo se puede utilizar si tiene una cuenta con membresía activa.
* Si ya pasó la hora específica o está en la hora justa, no se puede desagendar.
* No se podrá agendar horas con anticipación de mas de 2 meses. 

# 6.  Prioridades de Desarrollo

### Alta Prioridad
* Gestión de estado de membresía.
* Registro de ingresos/salidas.
* Agendamiento de horario.
* Registro de usuarios.

### Media Prioridad
* Dashboard administrativo.
* Control básico de acceso.

### Baja Prioridad
* Reportes avanzados.
* Integraciones adicionales.


# 7. Flujos Principales
**Flujo de Autentificación** 
* **Registro de Usuario:**

    1. El usuario presiona "Registrarse".
    2. Ingresa Datos (Nombre, RUT, email, contraseña).
    3. Acepta términos y condiciones.
    4. Acceder a la pantalla principal.
* **Inicio de Sesión (Login):**

    1. El usuario accede a la pantalla de login.
    2. Ingresa sus credenciales (email y contraseña).
    3. Presiona "Iniciar Sesión".
    4. Si es correcto, accede a la pantalla principal.
    5. Flujo Alternativo: Si las credenciales son incorrectas, se muestra un mensaje de error.
* 2.Flujo de Gestión de agendas
*   Reserva de gimnasio:
    1. El usuario navega a la seleccion de "Agendar"
    2. Selecciona los dias y horas disponibles
    3. Confirma Reserva
    4. Se le agrega en la pantalla principal
*   Cancelacion de reserva:
    1. El usuario accede a la pantalla principal
    2. Selecciona la reserva que desea cancelar 
    3. Confirma la cancelacion
    4. La Reserva se libera y el usuario recibe una notificacion
* 3.Flujo de Gestion de Membresía
*   Informacion membresia:
    1. El usuario accede a la seccion de "Membresia"
    2. Visualiza el estado de su membresia