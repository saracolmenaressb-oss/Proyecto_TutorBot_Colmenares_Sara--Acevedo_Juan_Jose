# Proyecto con n8n: TutorBot

Sistema Inteligente para la Gestión Automatizada de Tutorías Académicas

---------
## Integrantes:

- Sara Colmenares
- Juan Jose Acevedo

----------
## Descripción del problema:

En muchas instituciones educativas, el proceso para solicitar una tutoría académica continúa realizándose de forma manual mediante mensajes, llamadas o correos electrónicos. Esto provoca problemas como:
* Demoras en la asignación de tutores.
* Cruces de horarios entre estudiantes y tutores.
* Dificultad para conocer la disponibilidad real de cada tutor.
* Pérdida del historial de tutorías realizadas.
* Falta de seguimiento al estado de cada solicitud.
Como consecuencia, tanto estudiantes como coordinadores invierten demasiado tiempo organizando asesorías que podrían automatizarse.
Para solucionar esta problemática se desarrolla TutorBot, un sistema de automatización construido en n8n que utiliza WhatsApp como canal de comunicación con los estudiantes y Google Sheets como base de datos.
El sistema permite que un estudiante solicite una tutoría de forma automática, encuentre un tutor disponible según la materia y el horario, registre toda la información y mantenga actualizados los estados de cada tutoría.
----------
## Objetivo del problema:

- Desarrollar un sistema automatizado para la gestión de tutorías académicas mediante n8n, integrando WhatsApp y Google Sheets para facilitar la asignación inteligente de tutores, optimizar el uso de los recursos académicos y mejorar la experiencia de los estudiantes.

----------

## Descripción del sistema:

- TutorBot es un asistente conversacional que automatiza completamente el proceso de asignación de tutorías académicas.
El estudiante interactúa mediante WhatsApp, donde puede registrarse, solicitar una tutoría, consultar el estado de sus solicitudes o cancelar una reserva.
Toda la lógica del sistema es administrada por n8n, encargado de procesar los mensajes, consultar la base de datos, buscar tutores disponibles, registrar la información y enviar las notificaciones correspondientes.
La información del sistema se almacena en Google Sheets, lo que permite disponer de una base de datos sencilla, organizada y fácil de mantener.
-----------
## Tecnologías utilizadas:

* n8n
* Telegram
* Google Sheets
* Google Drive
* Webhooks
* JavaScript (Function Nodes)
-----------
## Funcionalidades principales:

El sistema permite:
* Registro automático de estudiantes.
* Solicitud de tutorías.
* Selección de materias.
* Consulta de disponibilidad.
* Asignación automática de tutores.
* Confirmación de tutorías.
* Cancelación de solicitudes.
* Consulta del estado de una tutoría.
* Envío de recordatorios automáticos.
* Registro histórico de todas las asesorías.
------------
## Base de datos:
La base de datos se implementa mediante Google Sheets y está organizada en varias hojas.

**ESTUDIANTES**

Almacena la información básica de los estudiantes.
Campos:
* id_estudiante
* nombre
* teléfono
* carrera
* semestre

**TUTORES**

Contiene los tutores disponibles.
Campos:
* id_tutor
* nombre
* materias
* estado

**DISPONIBILIDAD**

Registra los horarios disponibles de cada tutor.
Campos:
* id_disponibilidad
* id_tutor
* día
* hora_inicio
* hora_fin
* estado

**TUTORIAS:**

Guarda todas las tutorías solicitadas.
Campos:
* id_tutoria
* id_estudiante
* id_tutor
* materia
* fecha
* hora
* estado

**Estados posibles:**

* Solicitada
* Asignada
* Confirmada
* Finalizada
* Cancelada

**SESIONES:**

Permite mantener el estado de la conversación con cada usuario.
Campos:
* telefono_usuario
* pantalla_actual
* paso_actual
* datos_temporales
------------

## Flujo de funcionamiento
1. Inicio

El estudiante envía un mensaje por WhatsApp.

2. Registro

Si el estudiante no existe en la base de datos, el sistema solicita la información necesaria y realiza el registro.

3. Solicitud de tutoría: El sistema presenta el listado de materias disponibles.
------------

## capturas van aqui

Cuando termina la asesoría, el estado cambia a Finalizada.

Workflow desarrollado

(Agregar aquí las capturas del flujo de n8n.)

Capturas de WhatsApp

Agregar capturas de:

Registro
Solicitud de tutoría
Confirmación
Consulta de estado
Cancelación
Resultados esperados
-----------
## Con la implementación del sistema se espera:

* Reducir significativamente el tiempo de asignación de tutorías.
* Evitar conflictos de horarios.
* Automatizar completamente el proceso de asignación.
* Mantener un historial completo de todas las asesorías.
* Mejorar la comunicación entre estudiantes y tutores.
* Facilitar el seguimiento por parte de la coordinación académica.
* Posibles mejoras
* Integración con Google Calendar.
* Recordatorios automáticos antes de la tutoría.
* Panel administrativo web.
* Estadísticas de uso.
* Calificación del tutor por parte del estudiante.
* Integración con inteligencia artificial para responder preguntas frecuentes.
---------
## Conclusiones

El desarrollo de TutorBot demuestra cómo las herramientas de automatización pueden resolver procesos administrativos repetitivos dentro de una institución educativa.
Gracias a la integración entre WhatsApp, n8n y Google Sheets, fue posible diseñar un sistema capaz de gestionar solicitudes de tutorías de manera organizada, rápida y confiable, reduciendo el trabajo manual y mejorando la experiencia tanto de estudiantes como de tutores.
Además, la arquitectura implementada permite que el sistema pueda ampliarse fácilmente para incorporar nuevas funcionalidades, convirtiéndolo en una solución escalable para instituciones educativas con un gran número de usuarios.
