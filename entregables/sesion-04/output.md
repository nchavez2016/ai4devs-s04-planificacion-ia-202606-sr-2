Épica 1: Autenticación y Conexión Google
US01: Autenticación de usuario con Google OAuth
User Story: Como usuario profesional, quiero iniciar sesión en FlowSync usando mi cuenta de Google, para acceder a la aplicación de forma rápida y segura.

Criterios de Aceptación:

Scenario: Inicio de sesión exitoso por primera vez

Given que soy un usuario nuevo y visito la página de inicio de FlowSync

When hago clic en el botón "Iniciar sesión con Google" y autorizo los permisos solicitados

Then la aplicación crea mi cuenta, me redirige a la pantalla principal y muestra mi sesión activa.

Scenario: Flujo de retorno para usuario existente

Given que ya tengo una cuenta registrada en FlowSync y mi sesión ha expirado

When hago clic en "Iniciar sesión con Google" e ingreso mis credenciales

Then el sistema me redirige directamente a mi pantalla principal con mis tareas guardadas.

US02: Revocación de permisos y cierre de sesión
User Story: Como usuario de FlowSync, quiero cerrar mi sesión y desvincular mi cuenta, para proteger la privacidad de mis datos cuando no use la aplicación.

Criterios de Aceptación:

Scenario: Cierre de sesión básico

Given que estoy autenticado en FlowSync y en la pantalla principal

When selecciono la opción "Cerrar Sesión"

Then mi sesión actual se destruye y el sistema me redirige a la página de bienvenida pública.

Scenario: Revocación de acceso a Google Calendar (asumido)

Given que estoy en la configuración de mi perfil dentro de la aplicación

When hago clic en "Desconectar Google Calendar"

Then el sistema revoca el token de acceso de Google, elimina la sincronización activa y cambia el estado de la conexión a "Desconectado".

Épica 2: Gestión de Tareas (CRUD)
US03: Crear una tarea con atributos esenciales
User Story: Como usuario registrado, quiero crear una tarea con título, descripción opcional y fecha de vencimiento, para agendar mis pendientes del día.

Criterios de Aceptación:

Scenario: Creación de tarea con todos los campos

Given que estoy en la pantalla principal de la aplicación

When completo el formulario de creación con el título "Revisar reporte financiero", la descripción "Validar Q2" y la fecha de vencimiento "2026-07-01"

Then la tarea se guarda correctamente con estado pending (asumido) y se renderiza en la lista.

Scenario: Validación de campo obligatorio

Given que tengo el formulario de nueva tarea abierto

When intento guardar la tarea dejando el campo de título vacío

Then el sistema bloquea el envío y muestra un mensaje de error indicando que el título es obligatorio.

US04: Visualizar el listado de tareas pendientes y completadas
User Story: Como usuario, quiero ver todas mis tareas organizadas en una interfaz limpia, para evaluar rápidamente mi carga de trabajo actual.

Criterios de Aceptación:

Scenario: Renderizado de lista de tareas vacía

Given que soy un usuario nuevo sin tareas creadas y accedo a la pantalla principal

When carga la interfaz de usuario

Then el sistema muestra un mensaje indicando que no hay tareas pendientes y me invita a crear la primera.

Scenario: Visualización de tareas existentes

Given que tengo 5 tareas guardadas en la base de datos

When accedo a la pantalla principal

Then el sistema lista las 5 tareas mostrando claramente su título, fecha de vencimiento y estado actual.

US05: Actualizar los detalles de una tarea
User Story: Como usuario, quiero modificar la información de una tarea existente, para corregir errores o actualizar los detalles del pendiente.

Criterios de Aceptación:

Scenario: Modificación exitosa de atributos

Given una tarea existente titulada "Enviar correo" en mi listado

When abro la edición de la tarea, cambio el título a "Enviar correo a Gerencia" y guardo los cambios

Then la lista se actualiza inmediatamente mostrando el nuevo título en pantalla.

US06: Cambiar el estado de una tarea (Completar/Reabrir)
User Story: Como usuario, quiero marcar una tarea como completada o devolverla a pendiente, para mantener el control sobre lo que ya he ejecutado.

Criterios de Aceptación:

Scenario: Marcar tarea como completada

Given una tarea en estado pending en mi lista principal

When hago clic en el checkbox o botón de "Completar" de dicha tarea

Then el estado de la tarea cambia a completed y se aplica un estilo visual de tachado o archivado en la interfaz (asumido).

Scenario: Reabrir una tarea completada

Given una tarea en el listado con estado completed

When desmarco el checkbox de la tarea

Then el estado vuelve a cambiar a pending y se remueve el estilo visual de completada.

US07: Eliminar una tarea de forma definitiva
User Story: Como usuario, quiero borrar una tarea que ya no es necesaria, para mantener mi backlog limpio y libre de ruido.

Criterios de Aceptación:

Scenario: Eliminación de tarea con confirmación

Given una tarea visible en mi listado

When hago clic en el botón "Eliminar" y confirmo la acción en el mensaje emergente (asumido)

Then la tarea se remueve permanentemente del listado y de la base de datos.

Épica 3: Organización y Utilidades
US08: Filtrar tareas por estado y fecha
User Story: Como usuario con múltiples pendientes, quiero filtrar mis tareas por estado (Pendientes/Completadas) o por su fecha de vencimiento, para enfocarme solo en lo relevante del momento.

Criterios de Aceptación:

Scenario: Filtrado por estado pendiente

Given que tengo un listado mixto de 10 tareas (6 pendientes y 4 completadas)

When selecciono el filtro "Solo Pendientes"

Then la interfaz se actualiza para mostrar únicamente las 6 tareas en estado pending.

Scenario: Filtrado por fecha de vencimiento de hoy (asumido)

Given que tengo tareas con diferentes fechas asignadas

When aplico el filtro "Vencen Hoy"

Then el sistema oculta todas las tareas cuya fecha de vencimiento no coincida con el día en curso.

US09: Exportar tareas a formato CSV
User Story: Como usuario profesional, quiero exportar mi listado de tareas a un archivo CSV, para poder analizar mis datos en hojas de cálculo de forma externa.

Criterios de Aceptación:

Scenario: Descarga exitosa del archivo CSV

Given que tengo tareas registradas en mi cuenta

When hago clic en el botón "Exportar a CSV"

Then el sistema genera y descarga automáticamente un archivo ejecutable en formato .csv que contiene las columnas de título, descripción, fecha de vencimiento y estado de todas mis tareas.

Épica 4: Sincronización con Google Calendar
US10: Sincronizar automáticamente la creación de tareas hacia Google Calendar (FlowSync -> Google Calendar)
User Story: Como usuario integrado, quiero que al crear una tarea con fecha en FlowSync esta se refleje automáticamente en mi Google Calendar, para evitar agendar el mismo bloque de forma manual.

Criterios de Aceptación:

Scenario: Sincronización de nueva tarea con fecha

Given que tengo mi cuenta de Google Calendar vinculada exitosamente

When creo una nueva tarea en FlowSync con el título "Reunión de Sincronización" para el día de mañana

Then el sistema se conecta con la API de Google y crea un evento del tipo "todo el día" o bloque de tiempo predeterminado (asumido) en el calendario principal del usuario.

Scenario: Tarea creada sin fecha asignada

Given un usuario con calendario vinculado

When crea una tarea sin definir una fecha de vencimiento

Then la tarea se guarda localmente en FlowSync pero no genera ningún evento en Google Calendar.

US11: Sincronizar actualizaciones de tareas hacia Google Calendar
User Story: Como usuario, quiero que cualquier cambio de fecha, título o estado de una tarea en FlowSync se actualice en el evento correspondiente de Google Calendar, para mantener ambos sistemas en total paridad.

Criterios de Aceptación:

Scenario: Modificación de fecha de tarea sincronizada

Given una tarea que ya se encuentra vinculada a un evento de Google Calendar

When modifico la fecha de vencimiento de la tarea en FlowSync a una nueva fecha

Then el sistema actualiza de forma asíncrona o inmediata el evento de Google Calendar moviéndolo al nuevo día asignado.

Scenario: Sincronización al completar la tarea (asumido)

Given una tarea vinculada a un evento en Google Calendar

When marco la tarea como completada en FlowSync

Then el sistema actualiza el evento en Google Calendar, modificando el título agregando un prefijo "[Completado]" o eliminando el evento según la preferencia por defecto del MVP (asumido).