# Actividad 5: Metáforas de interfaz

| Dominio fuente | Elemento digital | Etiqueta o mensaje | Comportamiento | Riesgo |
|---|---|---|---|---|
| Agenda de pared del consultorio (organizacional/familiar) | Calendario semanal con casillas por hora y por fisioterapeuta | "Semana del 8 al 14 de septiembre" | Al tocar una casilla libre se abre el formulario de registro; las casillas ocupadas están bloqueadas al tacto. | Un paciente sin experiencia digital puede esperar poder "escribir encima" como en papel, en vez de tocar y navegar a un formulario. |
| Semáforo (familiar) | Indicador de color en cada horario | "Disponible" (verde) / "Reservado" (rojo) / "Pendiente de confirmación" (amarillo) | El color cambia en tiempo real según el estado guardado en el sistema; nunca se muestra un horario en dos colores a la vez. | El significado de los colores no es universal (daltonismo, o asociaciones culturales distintas al rojo/verde); debe reforzarse con texto, no solo color. |
| Mostrador de recepción (navegación) | Barra de pasos ("breadcrumb"): Inicio → Fisioterapeuta → Horario → Datos → Confirmación | "Paso 2 de 4: elige tu horario" | Permite avanzar y retroceder sin perder los datos ya ingresados, igual que un paciente puede volver al mostrador a corregir un dato antes de que lo atiendan. | Si el usuario retrocede varios pasos puede asumir (erróneamente) que todo se reinició, cuando en realidad sus datos previos siguen guardados. |
| Carpeta/expediente (organizacional) | Tarjeta de "Mi cita" con folio visible | "Cita #0231 — Confirmada" | Cada cita tiene un identificador persistente que se puede consultar, modificar o cancelar buscándolo, igual que una carpeta física con un número de expediente. | Un paciente puede perder o no anotar su folio y sentir que "no tiene cómo probar" que su cita existe si no hay otro método de búsqueda (ej. por nombre o teléfono). |

## 10. Problema de usabilidad que resuelve cada metáfora
- **Agenda de pared:** reduce la carga de aprendizaje porque reutiliza un modelo mental que el paciente y el personal ya conocen (una grilla de horarios), evitando enseñar un concepto nuevo desde cero.
- **Semáforo:** resuelve la falta de visibilidad del estado de un horario, que era el principal problema del proceso AS-IS (había que preguntar para saber si algo estaba libre).
- **Mostrador de recepción:** resuelve la pérdida de contexto al avanzar o retroceder en un flujo de varios pasos, evitando que el usuario deba reiniciar todo si se equivoca.
- **Carpeta/expediente:** resuelve la falta de un punto único de verdad sobre una cita, permitiendo consultarla después sin depender de recordar una conversación de WhatsApp.

## 11. Affordances, mapeo, consistencia y retroalimentación
- **Affordance:** las casillas libres se ven "presionables" (borde, sombra, cursor de mano); las ocupadas se ven deshabilitadas (opacidad reducida, sin sombra).
- **Mapeo:** la posición de cada casilla en la grilla corresponde exactamente a un día y una hora reales, igual que en una agenda física.
- **Consistencia:** el mismo código de color (verde/amarillo/rojo) se usa en todas las pantallas donde aparece un horario o el estado de una cita.
- **Retroalimentación:** toda acción (seleccionar horario, confirmar, cancelar) muestra una respuesta inmediata en pantalla (cambio de color, mensaje de confirmación, spinner de carga) antes de dejar avanzar al siguiente paso.

## 12. Estados, reglas, validaciones y persistencia
- **Estados de una cita:** disponible → seleccionada (temporal) → confirmada → (modificada | cancelada | reagendada).
- **Regla:** un horario en estado "seleccionada" se bloquea temporalmente (ej. 5 minutos) para evitar que dos personas lo reserven a la vez mientras uno completa el formulario.
- **Validación:** no se permite confirmar una cita si el horario cambió de estado (por otra reserva) entre que se mostró y que se confirmó; el sistema debe re-verificar antes de guardar.
- **Persistencia:** cada cita guarda folio, paciente, fisioterapeuta, horario y estado, de forma que puede consultarse después sin depender de que el chat de WhatsApp siga existiendo.

## 13. Límites o riesgos culturales
- **Agenda de pared:** asume que el usuario entiende el concepto de "semana calendario"; puede no ser intuitivo para quien nunca usó una agenda física ni digital.
- **Semáforo:** el rojo/verde no es universal (algunas culturas o personas con daltonismo no lo interpretan igual); se mitiga con etiquetas de texto.
- **Mostrador de recepción:** el patrón de "pasos numerados" es común en apps occidentales de reservas, pero un usuario mayor sin experiencia digital previa puede no reconocer la convención y necesitar apoyo adicional.
- **Carpeta/expediente:** el uso de un "folio" o número puede generar desconfianza en pacientes acostumbrados a un trato personal y verbal, si no se acompaña con el nombre del fisioterapeuta y la fecha en texto claro.
