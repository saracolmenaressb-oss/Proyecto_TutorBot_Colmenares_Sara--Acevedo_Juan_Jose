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
El estudiante interactúa mediante telegram, donde puede registrarse, solicitar una tutoría, consultar el estado de sus solicitudes o cancelar una reserva.
Toda la lógica del sistema es administrada por n8n, encargado de procesar los mensajes, consultar la base de datos, buscar tutores disponibles, registrar la información y enviar las notificaciones correspondientes.
La información del sistema se almacena en Google Sheets, lo que permite disponer de una base de datos sencilla, organizada y fácil de mantener.
-----------
## Tecnologías utilizadas:

* n8n
* Telegram
* Google Sheets
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

**ESTUDIANTES:**

Almacena la información básica de los estudiantes.
Campos:
* chat_id
* estado
* paso
* updated_at

**TUTORES:**

Contiene los tutores disponibles.
Campos:
* id_tutor
* nombre
* especialidad_materia
* whatsapp
* email
* estado

**DISPONIBILIDAD**

Registra los horarios disponibles de cada tutor.
Campos:
* id_dispo
* id_tutor
* dia_semana
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
* created_a

**Estados posibles:**

* Solicitada
* Asignada
* Confirmada
* Finalizada
* Cancelada

**SESIONES:**

Permite mantener el estado de la conversación con cada usuario.
Campos:
* whatsapp
* pantalla_actual
* paso_actual
* datos_parciales
* updated_at

------------

## Flujo de funcionamiento de n8n:

En primer lugar, el nodo “Espera de respuesta” recibe el mensaje enviado por el usuario desde Telegram. A continuación, el nodo de código en JavaScript extrae de forma segura los datos más importantes del mensaje, como el chat_id, que identifica la conversación para poder responder al usuario, y el texto del mensaje, que contiene la solicitud realizada. Además, el código valida que la información recibida sea correcta; si no encuentra el identificador del chat, genera un error para evitar que el flujo continúe con datos incompletos.

Posteriormente, el flujo consulta la base de datos, almacenada en una hoja de cálculo, con el fin de verificar si el estudiante ya se encuentra registrado en el sistema. Después de leer los registros, un segundo bloque de código analiza la información obtenida para determinar si el usuario es nuevo o si ya existe en la base de datos.

Con base en esta validación, el nodo If toma una decisión. Si el estudiante no está registrado, el flujo ejecuta el nodo “Agregar nuevo usuario”, el cual almacena sus datos en la base de datos para que pueda utilizar el sistema en futuras ocasiones. Si el estudiante ya existe, el flujo continúa sin necesidad de volver a registrarlo.

Finalmente, el flujo utiliza un nodo Switch para identificar la intención del mensaje enviado por el usuario. Dependiendo de la opción seleccionada o del texto recibido, el sistema envía una respuesta automática correspondiente, como mostrar el menú principal, solicitar una tutoría, consultar una tutoría ya registrada o cancelar una tutoría. En caso de que el mensaje no coincida con ninguna opción válida, el bot responde indicando que la opción no fue reconocida.

Cuando el estudiante solicita una tutoría, el sistema consulta la base de datos donde se encuentran registrados los profesores, junto con sus horarios y días disponibles, para ofrecer únicamente las opciones que realmente están disponibles. De esta manera, el proceso de asignación de tutorías se realiza de forma automática, reduciendo el tiempo de atención y evitando la intervención manual.

En conjunto, este flujo integra Telegram, JavaScript y una base de datos en hojas de cálculo para gestionar el registro de estudiantes, verificar su existencia en el sistema, consultar la disponibilidad de profesores y responder automáticamente a las solicitudes de tutorías, haciendo que el proceso sea más rápido, organizado y eficiente.

------------

## Evidencias: 

**Capturas de Telegram**

![alt text](img/inicio.jpeg)

![alt text](img/opcion1.jpeg)

![alt text](img/materia1.jpeg)

![alt text](img/fecha1.jpeg)

![alt text](img/buscar.jpeg)

![alt text](img/tutor.jpeg)

![alt text](img/opcion2.jpeg)

![alt text](img/tutoria.jpeg)

![alt text](img/opcion3.jpeg)

![alt text](img/cancelar.jpeg)

![alt text](img/cancelado.jpeg)

![alt text](img/error1.jpeg)

-----------

**Workflow desarrollado**

* Flujo de n8n:

![alt text](img/flujo-completo.jpeg)

![alt text](img/workflow1.jpeg)

![alt text](img/workflow2.jpeg)

![alt text](img/workflow3.jpeg)

![alt text](img/workflow4.jpeg)

-------

**Bases de datos:**

![alt text](img/tabla1.jpeg)

![alt text](img/imagen2.jpeg)

![alt text](img/tabla3.jpeg)


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
