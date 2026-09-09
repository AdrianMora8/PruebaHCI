# Actividad 4: Operacionalizar la eficiencia

**Responsable:** Julio Jacho

**Variable dependiente:** Eficiencia del proceso de agendamiento: grado en que una operación se completa correctamente utilizando menor tiempo y esfuerzo humano, sin incrementar errores ni reprocesos.

| Operación | Inicio | Final | Indicadores seleccionados |
|---|---|---|---|
| Consultar disponibilidad | El usuario abre la vista de horarios de un fisioterapeuta. | Se muestra la lista de horarios libres/ocupados en pantalla. | (1) N.º de clics/pasos hasta ver el resultado; (2) tasa de consultas que no requieren contacto adicional con el personal. |
| Registrar una cita | El paciente o el personal selecciona un horario disponible. | La cita queda guardada con estado "confirmada" y visible para el fisioterapeuta. | (1) Tasa de registros exitosos al primer intento (sin reprocesos); (2) n.º de citas dobles o en conflicto detectadas y bloqueadas por el sistema. |
| Modificar una cita | El usuario abre una cita existente y elige "modificar". | La cita queda actualizada con el nuevo dato y notificación enviada a las partes afectadas. | (1) N.º de acciones necesarias para completar el cambio; (2) tasa de modificaciones que requieren intervención manual del personal. |
| Cancelar una cita | El usuario selecciona "cancelar" sobre una cita existente. | La cita queda marcada como cancelada y el horario vuelve a estar disponible. | (1) Tasa de cancelaciones confirmadas sin error (horario liberado correctamente); (2) tiempo entre la cancelación y la disponibilidad real del horario liberado. |
| Reagendar una cita | El usuario elige "reagendar" sobre una cita existente. | La cita anterior queda cancelada y una nueva cita queda registrada, en una sola operación. | (1) Tasa de reagendamientos completados sin pasar por dos pasos separados (cancelar + registrar); (2) n.º de errores de duplicidad detectados durante el reagendamiento. |

## Justificación de no usar solo el tiempo

Un proceso puede ser rápido y aun así ineficiente si genera errores que obligan a un reproceso (por ejemplo, una cita registrada en el horario equivocado que debe corregirse después). Por eso cada operación combina un indicador de **pasos/acciones observables** con un indicador de **tasa de error o reproceso**, siguiendo la definición de la variable dependiente.
