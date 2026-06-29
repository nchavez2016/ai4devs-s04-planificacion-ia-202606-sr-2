He tomado la èpica 4 ,US10 y  se identificado los siguientes puntos ciegos.

1. Gestión de fallos de red/API: El criterio asume que la API de Google responderá con éxito siempre. No define qué pasa en la interfaz o con la tarea si la API de Google da un error de rate limit o no está disponible (el PRD exige que se guarde localmente y se reintente más tarde).

2. Definición de horas y Zonas Horarias: El criterio asume un "bloque de tiempo predeterminado" o "todo el día", pero el PRD alerta explícitamente que la relación entre la fecha límite de la tarea y la hora del evento en el calendario es un riesgo crítico que puede crear eventos a horas erróneas.

3. Mapeo de IDs para sincronización posterior: No se menciona que el sistema debe almacenar el ID del evento retornado por la API de Google vinculado a la tarea de FlowSync, lo cual es una dependencia técnica indispensable para poder cumplir con la posterior edición o eliminación descrita en el PRD.

4. Comportamiento ante desconexión OAuth: No se especifica qué ocurre si el token de Google expira o si el usuario revoca los permisos en Google Cloud justo en el momento de guardar la tarea.
