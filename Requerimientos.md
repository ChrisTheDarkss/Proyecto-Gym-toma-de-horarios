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
* Bloqueo/permiso de acceso desde aplicación.
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

* **Pago Inicial (Anticipo):** Se realizará un primer pago de **1.232.800 CLP** al momento de la firma de este documento.
* **Segundo Pago (Hito 50%):** Se realizará un segundo pago de **2.465.600 CLP** al completar el 50% de avance del proyecto.
* **Pago Final (Entrega):** Se pagará el saldo final de **2.465.600 CLP** con la entrega del software (MVP) funcional.

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

### Fase 1: Levantamiento de Requerimientos y Diseño Inicial

Duración: hasta el 21 de octubre

* Validación de requerimientos. 
* Planificación de sprints semanales y reuniones de seguimiento.

### Fase 2: Desarrollo del MVP  Funcionalidades Básicas

Duración: noviembre  
Entrega del primer prototipo estimada: Finales de noviembre

Semana 1 y 2:
* Equipo: Configuración del backend conexión a MongoDB.
* Maquetación inicial del frontend (login, registro, dashboard).
* Implementación inicial del sistema (simulada) y control de acceso.

Semana 3 y 4:
* Equipo: Implementación de CRUD de usuarios y membresías con reglas de estado.
*  Desarrollo de perfil de usuario, historial de accesos y vista de membresía.
*  Backend de agendamiento y aplicación de reglas de negocio.
*  Pruebas sobre funcionalidad de agendamiento y validación de restricciones.

### Fase 3: Consolidación y Entrega del MVP

Duración: diciembre  
Entrega del MVP funcional estimada: inicios diciembre

Semana 1:
* Equipo: Desarrollo de API para entrada/salida. 
*  Implementación de dashboard administrativo (funciones básicas).
*  Funcionalidad para bloquear o permitir acceso desde la aplicación.
*  Ejecución de pruebas completas con todos los roles del sistema.

Semana 2:
* Todos: Refactorización del código, mejora de funcionalidades y preparación para entrega.
*  Redacción de manuales de usuario, documentación técnica y resolución de errores.

### Fase 4: Soporte y Mantenimiento

Duración: enero a marzo

* Soporte técnico durante tres meses posteriores a la entrega.
* Revisión de errores y mejoras menores.
* Reuniones de seguimiento cada dos semanas.

## Stack Tecnológico Propuesto

### Backend
* **Entorno de ejecución:** Node.js.
* **Framework:** Express.js.
* **ODM (Object Data Modeling):** Mongoose (Para interactuar de forma segura con MongoDB).
* **Caché:** Redis (Para optimizar la velocidad de consultas frecuentes).

### Frontend
* **Librería:** React.js.

### Base de Datos
* **Sistema:** MongoDB.

### Autenticación
* **Método:** JWT (JSON Web Tokens).

### Plataformas de Despliegue (Hosting)
* **Backend (API):** Render.
* **Frontend:** Vercel.
* **Base de Datos:** MongoDB Atlas.

## Reuniones y Seguimiento

* Reunión semanal para revisión de avances y planificación
* Duración estimada: entre 30 y 45 minutos
* Canal sugerido: videollamada o reunión presencial

# 12. Soporte y Mantenimiento

* El sistema contará con un periodo de **soporte técnico gratuito de tres (3) meses posteriores a la entrega del proyecto**.  
* Durante este periodo se incluirá:  
  * **Corrección de errores** y fallas detectadas en el funcionamiento normal del sistema.  
  * **Asistencia técnica** para la instalación, configuración o uso general de la aplicación.  
  * **Ajustes menores o mejoras de mantenimiento** que no impliquen el desarrollo de nuevas funcionalidades.  
  * **Atención prioritaria a fallas críticas**, garantizando solución sin costo adicional.  
* El soporte será brindado mediante **correo electrónico o reuniones virtuales**, según acuerdo con el cliente.  
* Finalizado el periodo de soporte gratuito, el cliente podrá optar por un **contrato de mantenimiento extendido**, que cubra actualizaciones, mejoras o ampliaciones del sistema según sus necesidades futuras.  