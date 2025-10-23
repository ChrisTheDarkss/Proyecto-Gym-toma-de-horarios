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

# 3. Definición del MVP- Versión 1.0 (Incluye):

* El MVP se centra en las funcionalidades esenciales para la gestión operativa.

### Funcionalidades Core:

* Registro de usuarios con datos básicos.
* Gestión de membresías (estados: activa, expirada, suspendida).
* Agendamiento básico de horarios.
* Bloqueo/permiso de acceso desde aplicación(Control Básico).
* Registro de entrada y salida(Control de asistencia ). 

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
* No se podrán agendar horas si no quedan cupos disponibles.
* Si ya pasó la hora específica o está en curso, no se podrá cancelar ni modificar la reserva.
* Toda reserva será automáticamente cancelada y liberada si la membresía del usuario se encuentra inactiva (expirada o suspendida).
* No se permitirá el acceso al gimnasio si la membresía del usuario está expirada o suspendida. El sistema debe validar automáticamente el estado de la membresía en cada registro de entrada.
* El sistema deberá garantizar la persistencia de los datos frente a cortes de energía o fallas del servidor.
* En caso de corte eléctrico prolongado, el sistema mostrará un mensaje informando la indisponibilidad temporal.
* Los registros de entrada y salida con más de 12 meses de antigüedad serán archivados automáticamente en una colección separada para optimizar el rendimiento de la base de datos.
* No se podrá registrar una salida si el usuario no posee una entrada activa registrada el usuario tendrá que hablar con staff para agregar la entrada manualmente.
* Un usuario no puede tener más de una reserva activa en el mismo horario y día. 
El sistema debe rechazar reservas duplicadas para un mismo usuario en un mismo slot horario.

# 6.  Prioridades de Desarrollo

### Alta Prioridad
* Gestión de estado de membresía.
* Registro de ingresos/salidas.
* Agendamiento de horario.
* Registro de usuarios.
* Validación automática de membresías en acceso.

### Media Prioridad
* Dashboard administrativo.
* Control básico de acceso.
* Sistema de notificaciones básico (email):
    confirmación de reserva, recordatorio de cita, 
    cancelación, membresía por expirar

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
* **Flujo de Gestión de agendas:**
    * **Reserva de gimnasio:**
    1. El usuario navega a la selección de "Agendar".
    2. Selecciona los días y horas disponibles.
    3. Confirma Reserva.
    4. Se le agrega en la pantalla principal.
*   **Cancelación de reserva:**
    1. El usuario accede a la pantalla principal.
    2. Selecciona la reserva que desea cancelar. 
    3. Confirma la cancelación.
    4. La Reserva se libera y el usuario recibe una notificación.
*   **Información membresía:**
    1. El usuario accede a la sección de "membresía".
    2. Visualiza el estado de su membresía.
  
# 8. Requisitos Funcionales & No Funcionales

## Requisitos Funcionales 
* Registro de usuarios con datos básicos .
* Gestión de membresías (estados: activa, expirada, suspendida).
* Agendamiento básico de horarios por piso.
* Bloqueo/permiso de acceso al usuario.
* Registro de entrada y salida.
* Sistema de autenticación.


## Requisitos no funcionales 
* Seguridad de los datos de los usuarios.
* La aplicación funcionará en cualquier dispositivo que tenga acceso a un navegador con internet. 
* El usuario podrá agendar una hora y la solicitud se procesará en menos de 5 segundos. 

# 9. Plazos establecidos 
* Entrega de requisitos 21/10
* Primer prototipo ?/11
* Entrega de MVP funcional ?/12 

# 10. Alcance y Presupuesto
El sistema busca automatizar la gestión de un gimnasio, centralizando el control de usuarios, membresías, horarios y accesos mediante una base de datos NoSQL (MongoDB).
 
 La primera versión (MVP) incluirá los módulos esenciales:
* Registro y autenticación de usuarios.
* Gestión de membresías (activas, expiradas, suspendidas).
* Agendamiento y cancelación de horarios.

 El sistema podrá implementarse en:
* Gimnasios municipales (uso público con control de aforo y membresías).
* Gimnasios privados (pequeñas cadenas o centros independientes).
* Centros deportivos educativos (liceos, universidades, academias).
## Presupuesto
La estructura de pagos del proyecto es la siguiente:

**Lider de proyecto/Full Stack Developer:** Arquitectura, backend(API REST) y coordinacion  con una Salario 851.250 CLP por 113.5 Hrs. de trabajo.

**Desarrollador Full Stack:** Frontend(interfaces de usuario), flujo de cliente y dashboard con un salario de 731.250 CLP por 97,5 Hrs de trabajo.

**Desarollo Full Stack/QA:** Pruebas (QA), integracion y revisión de control de acceso con un salario de 686.250 CLP por 91,5 Hrs de trabajo.

**Tarifa Desarrollador: 7.500 CLP/Hrs**

**Costo total del proyecto:** Desarrollo del MVP es de 3.000.000 CLP  (400 Horas de trabajo estimadas).
* **Pago Inicial (Anticipo):** Se realizará un primer pago de **900.000 CLP** al momento de la firma de este documento.
* **Segundo Pago (Hito 50%):** Se realizará un segundo pago de **1.200.000 CLP** al completar el 50% de avance del proyecto(Backend + Frontend integrado y básico).
* **Pago Final (Entrega):** Se pagará el saldo final de **900.000 CLP** con la entrega del software (MVP) funcional.

## Costos operativos 
**Plan initial** 
* Backend Render Plan "Starter" Costo $7 USD / Mes.
* Base de Datos MongoDB Atlas: Plan "M2" Costo $9 USD / Mes.
* Caché Render Redis: Plan "Starter" Costo $10 USD / Mes. 

**Plan advance**
* Backend Render: Plan "Junior" Costo $15 USD / Mes.
* Base de Datos MongoDB Atlas: Plan "M3" Costo $57 USD / Mes.
* Caché (Render Redis): Plan "Junior" Costo $10 USD / Mes.

Los costos operacionales son mensuales y no están incluidos en los costos del proyecto y serán pagados por el cliente.


## Futuras Versiones (Excluye del MVP)

### Versión 2.0:

* **Notificaciones push y recordatorios**.
* **Reportes avanzados y analytics** (métricas de uso, ocupación, ingresos).
* Sistema de **reserva de equipos** específicos.
* **Planes de entrenamiento personalizados** (asignados por el staff/entrenador).

### Versión 3.0: 

* Sistema de logros y gamificación
* Chat interno con entrenadores
* Control de progreso físico


# 11. Propuesta y Forma de Trabajo

## Objetivo del Proyecto

* Desarrollar un sistema web basado en base de datos NoSQL (MongoDB) para gestionar integralmente un gimnasio. El sistema permitirá controlar usuarios, membresías, horarios y accesos de forma eficiente y escalable, mejorando la experiencia del cliente y optimizando los procesos internos del gimnasio.

## Distribución del Equipo y Roles

**Cristóbal Escobar**
* **Rol:** Líder de Proyecto / Full Stack Developer
* **Responsabilidades:**
    * Coordinación general del proyecto.
    * Arquitectura del sistema y diseño de la base de datos.
    * Desarrollo de la API REST y lógica de negocio (Backend).

**Sebastián Flores**
* **Rol:** Desarrollador Full Stack
* **Responsabilidades:**
    * Desarrollo de interfaces de usuario (Frontend).
    * Implementación de flujos de cliente (Login, registro, perfil).
    * Apoyo en lógica de agendamiento y Backend.

**Guido Bardi**
* **Rol:** Desarrollador Full Stack
* **Responsabilidades:**
    * Desarrollo de interfaces de administración (Frontend).
    * Implementación del Dashboard administrativo.
    * Apoyo en lógica de control de acceso y Backend.

**Vicente Saavedra**
* **Rol:** Desarrollador Full Stack
* **Responsabilidades:**
    * Encargado de Pruebas (QA) y testing de flujos.
    * Apoyo en la integración de frontend y backend.
    * Revisión de control de acceso.

## Roadmap del Proyecto

* **Fase 1 (hasta 24/10)**: Levantamiento de Requerimientos y Diseño Inicial.
* **Fase 2 (Noviembre)**: Desarrollo del MVP Funcionalidades Básicas (Backend, conexión Base de Datos, CRUD, Agendamiento).
* **Fase 3 (Diciembre)**: Consolidación y Entrega del MVP (API entrada/salida, Dashboard básico, Pruebas finales, Documentación).
* **Fase 4 (Enero a Marzo)**: Soporte y Mantenimiento.

## Stack Tecnológico Propuesto

### Backend
* **Entorno de ejecución:** Node.js.
* **Framework:** Express.js.
* **ODM (Object Data Modeling):** Mongoose (Para interactuar de forma segura con MongoDB).
* **Caché:** Redis (Para optimizar la velocidad de consultas frecuentes).

### Frontend
* **Librería:** React.js.

### Base de Datos y Backup
* **Sistema:** MongoDB(Backup Snapshots).

### Autenticación
* **Método:** JWT (JSON Web Tokens).

### Plataformas de Despliegue (Hosting)
* **Backend (API):** Render.
* **Frontend:** Vercel.
* **Base de Datos:** MongoDB Atlas.

### Para garantizar la seguridad de los datos del gimnasio:

* **Backups Automáticos:** Copias de seguridad semanales de la base de datos.

* **Plataforma:** Usaremos el servicio integrado de MongoDB Atlas.

* **Retención:** Conservaremos backups de los últimos 30 días.

* **Recuperación:** Posibilidad de restaurar datos en caso de eliminación accidental o fallos del sistema.

## Reuniones y Seguimiento

* Reunión semanal para revisión de avances y planificación
* **Duración estimada:** entre 30 y 45 minutos
* **Canal:** videollamada o reunión presencial

# 12. Soporte y Mantenimiento

* El sistema contará con un periodo de **soporte técnico gratuito de tres (3) meses posteriores a la entrega del proyecto**.  
* Durante este periodo se incluirá:  
  * **Corrección de errores** y fallas detectadas en el funcionamiento normal del sistema.  
  * **Asistencia técnica** para la instalación, configuración o uso general de la aplicación.  
  * **Ajustes menores o mejoras de mantenimiento** que no impliquen el desarrollo de nuevas funcionalidades.  
  * **Atención prioritaria a fallas críticas**, garantizando solución sin costo adicional.  
* El soporte será brindado mediante **correo electrónico o reuniones virtuales**, según acuerdo con el cliente.  
* Finalizado el periodo de soporte gratuito, el cliente podrá optar por un **contrato de mantenimiento extendido**, que cubra actualizaciones, mejoras o ampliaciones del sistema según sus necesidades futuras.  