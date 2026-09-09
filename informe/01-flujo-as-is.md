# Actividad 1: Análisis del proceso actual (AS-IS)

## 1.1 Flujo actual

| Paso | Acción actual | Medio | Actor(es) | Información necesaria | Decisión tomada |
|---|---|---|---|---|---|
| 1 | El paciente solicita una cita. | WhatsApp | Paciente | Motivo de consulta, disponibilidad propia | Elegir a quién escribir (no hay un canal único) |
| 2 | El personal revisa los mensajes y consulta disponibilidad. | WhatsApp y agenda física | Personal administrativo | Historial de chats, agenda física de 5 fisioterapeutas | Qué horarios ofrecer |
| 3 | Se coordina el horario con el fisioterapeuta. | Conversación o revisión manual | Personal administrativo, Fisioterapeuta | Disponibilidad real del fisioterapeuta, tipo de tratamiento | Confirmar o proponer otro horario |
| 4 | La cita se registra y se confirma al paciente. | Agenda física y WhatsApp | Personal administrativo | Datos del paciente, horario acordado | Registrar en agenda física y responder al paciente |
| 5 | Los cambios o cancelaciones se procesan manualmente. | WhatsApp y agenda física | Paciente, Personal administrativo | Cita original, nuevo horario (si aplica) | Tachar/reescribir en agenda, avisar al fisioterapeuta |

## 1.2 Esperas, transcripciones, duplicaciones y errores

- **Esperas:** el paciente espera respuesta en WhatsApp sin saber cuánto tiempo tomará; el personal debe revisar mensajes acumulados antes de poder responder.
- **Transcripciones:** la información viaja de WhatsApp → memoria/agenda física → posible traspaso verbal al fisioterapeuta. Cada transcripción es un punto de pérdida o alteración de datos.
- **Acciones duplicadas:** el personal debe consultar dos fuentes distintas (chat de WhatsApp y agenda física) para saber si un horario está libre, y luego volver a escribir el mismo dato en ambos lugares al confirmar.
- **Errores posibles:** doble reserva de un mismo horario (dos pacientes distintos negociando en paralelo por WhatsApp), pérdida de mensajes antiguos en el chat, letra ilegible o tachones en la agenda física, falta de aviso a un fisioterapeuta sobre un cambio.

## 1.3 Problemas de retroalimentación, visibilidad y consistencia

- **Retroalimentación:** el paciente no tiene forma de saber si su solicitud está "pendiente", "en revisión" o "confirmada" mientras el personal no responda manualmente.
- **Visibilidad:** no existe una vista consolidada de la disponibilidad de los 5 fisioterapeutas; la agenda física es un objeto único que solo puede consultar una persona a la vez.
- **Consistencia:** el mismo dato (horario de una cita) puede existir de forma distinta en WhatsApp (texto libre) y en la agenda física (anotación manual), sin mecanismo que las mantenga sincronizadas.

## 1.4 Factores humanos y tecnológicos

**Factores humanos:**
1. Carga cognitiva del personal administrativo al sostener múltiples conversaciones de WhatsApp en paralelo y cruzarlas mentalmente contra la agenda física.
2. Dependencia de la memoria y disciplina individual del personal para no olvidar confirmar, actualizar o avisar cambios a los fisioterapeutas.

**Factores tecnológicos:**
1. WhatsApp no fue diseñado para gestión de citas: no tiene estados, ni bloqueo de horarios, ni alertas de conflicto.
2. La agenda física es un medio no replicable ni respaldable: un daño, pérdida u error de escritura no tiene forma de recuperarse ni auditarse.
