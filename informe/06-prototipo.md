# Actividad 6: Prototipo navegable

**Herramienta:** Figma
**Enlace del prototipo:** [GABO'S - Prototipo Gestión de Citas](https://www.figma.com/design/5Wb9weDs7bpY1WdUnVrif9/GABO-S---Prototipo-Gesti%C3%B3n-de-Citas?node-id=0-1&t=CZsZQNrpiL6RdLAU-1)

## 0. Decisiones de diseño

- **Mobile-first.** Actualmente, los pacientes agendan por WhatsApp desde el celular; por ello, el prototipo prioriza pantallas de 360-390 px de ancho. Esta decisión evita introducir un cambio de dispositivo además del cambio de canal.
- **Mecanismo híbrido (Actividad 8).** La mayoría de las citas se confirma automáticamente, mientras que los casos que requieren criterio del personal pasan al estado **"Pendiente de revisión"**. Así, el comportamiento del prototipo se mantiene alineado con la recomendación del equipo.
- **Terminología única:** se usa siempre la palabra **"cita"** (nunca "turno" ni "reserva") en toda pantalla, botón y mensaje, para ser consistente con el dominio real del centro y con la metáfora de agenda (Actividad 5).
- **Perfil del usuario principal (Actividad 2):** pacientes de fisioterapia, con posible movilidad reducida y perfil tecnológico heterogéneo (desde jóvenes hasta adultos mayores). Esto obliga a: textos claros sin jerga técnica, objetivos táctiles grandes, y ninguna interacción que dependa de precisión motriz fina (nada de arrastrar/soltar).

## 1. Mapa de navegación (arquitectura de información)

```
Inicio
 ├─→ Agendar nueva cita
 │     ├─→ Consulta de disponibilidad
 │     │     └─→ Selección de fisioterapeuta
 │     │           └─→ Registro de datos del paciente
 │     │                 └─→ Resumen y confirmación
 │     │                       └─→ [horario ocupado] Error: horario no disponible
 │     │                       ├─→ [caso normal] Cita confirmada (éxito)
 │     │                       └─→ [caso excepción] Solicitud en revisión
 │     └─→ (sin horarios disponibles) Estado vacío con alternativa
 └─→ Mis citas (lista)
       └─→ Detalle de una cita existente
             ├─→ Reagendar → vuelve a Consulta de disponibilidad (con datos precargados)
             └─→ Cancelar → Confirmación de cancelación → Cita cancelada (con opción deshacer)

Accesible desde cualquier pantalla: "¿Necesitas ayuda?" → Contacto directo con el centro
```

Toda pantalla dentro del flujo de agendar conserva la barra de pasos (Actividad 5) y un botón "Atrás" explícito además del gesto/botón nativo, para que "adelante y atrás sin pérdida de información" sea verificable por dos vías, no solo una.

## 2. Pantallas del prototipo

**Las pantallas principales del prototipo (01-11):**

1. **Inicio** de gestión de citas.
2. **Disponibilidad** de horarios.
3. **Selección de fisioterapeuta**.
4. **Registro de datos** del paciente.
5. **Resumen y confirmación** de la cita.
6. **Error: horario no disponible**, cuando el cupo se ocupa antes de confirmar.
7. **Cita confirmada**, para el caso normal.
8. **Solicitud en revisión**, para el caso que requiere coordinación del personal.
9. **Detalle de cita** existente.
10. **Reagendar cita**, con confirmación del nuevo horario.
11. **Cancelar cita**, mediante un diálogo de confirmación.

La ayuda/contacto se mantiene como acceso transversal del flujo, no como una pantalla numerada independiente.
La lista "Mis citas" funciona como punto de acceso al detalle, pero no aparece como frame independiente numerado en el Figma compartido.

## 3. Especificación detallada por pantalla

### 1. Inicio
- **Elementos:** saludo breve, botón primario "Agendar nueva cita", botón secundario "Mis citas", acceso a "¿Necesitas ayuda?".
- **Estado vacío (primera vez):** si el paciente no tiene citas previas, "Mis citas" muestra 0 sin error ("Aún no tienes citas registradas").
- **Heurística:** reconocimiento antes que recuerdo — no exige que el paciente sepa comandos, solo dos acciones visibles.

### 2. Consulta de disponibilidad
- **Elementos:** grilla semanal, semáforo de 3 estados (verde=disponible, amarillo=pendiente/bloqueado temporalmente, rojo=ocupado), selector de semana (flechas adelante/atrás), filtro opcional por fisioterapeuta.
- **Estado vacío:** si una semana completa no tiene cupos, mostrar mensaje "No hay horarios esta semana" + botón "Ver siguiente semana" (nunca una grilla en blanco sin explicación).
- **Regla de concurrencia:** al tocar un horario verde, cambia a amarillo ("reservado temporalmente, 5 min") solo para ese usuario; si no completa el flujo en ese tiempo, vuelve a verde para todos. Debe verse un contador visible, no un límite oculto (control y libertad del usuario).

### 3. Selección de fisioterapeuta
- **Elementos:** tarjeta por fisioterapeuta (nombre, especialidad/enfoque, foto genérica, disponibilidad resumida del horario ya elegido).
- **Caso límite:** si el horario elegido solo lo atiende un fisioterapeuta, saltar esta pantalla automáticamente y mostrarlo preseleccionado (eficiencia, no forzar un paso vacío).

### 4. Registro de datos del paciente
- **Campos:** nombre completo, teléfono, motivo de consulta (texto corto), **checkbox: "Es mi primera vez / tengo una condición que requiere coordinación especial"**.
- **Por qué el checkbox:** es el gatillo concreto del mecanismo híbrido — si se marca, el flujo termina en "Solicitud en revisión" en vez de confirmación automática.
- **Validación:** en línea, por campo, al perder el foco (no solo al enviar); mensaje de error específico ("Ingresa un teléfono válido de 10 dígitos"), nunca genérico ("Error").
- **Persistencia:** si el paciente retrocede desde el Resumen, estos datos siguen ahí.

### 5. Resumen y confirmación
- **Elementos:** fisioterapeuta, fecha, hora, datos del paciente, botón primario "Confirmar cita", botón secundario "Editar".
- **Antes de confirmar:** revalidación silenciosa de que el horario sigue libre (si ya no, ver mensaje de error de la sección 6, no un fallo silencioso).
- **Bifurcación:** según el checkbox del paso 4 → pantalla 7, "Cita confirmada", o pantalla 8, "Solicitud en revisión".

### 6. Error: horario no disponible
- **Condición:** el horario seleccionado deja de estar disponible antes de confirmar la cita.
- **Mensaje:** se informa claramente que otra persona reservó el horario y se solicita elegir uno nuevo; los datos ya ingresados se conservan.
- **Acción:** el botón de regreso lleva nuevamente a la disponibilidad para seleccionar otro horario.

### 7. Cita confirmada
- **Elementos:** confirmación visual de éxito, datos de la cita, fisioterapeuta, fecha, hora y folio.
- **Acción principal:** botón para consultar la cita en "Mis citas" o ver su detalle.
- **Propósito:** hacer visible el resultado de la operación y evitar que el paciente dude si la cita fue registrada.

### 8. Solicitud en revisión
- **Mensaje:** "Recibimos tu solicitud. El personal la revisará y te contactaremos para confirmar."
- **Elementos:** folio de seguimiento, estado "Pendiente", datos de la cita solicitada y botón "Ver mi solicitud".
- **Persistencia:** aparece también en "Mis citas" con el semáforo amarillo; nunca desaparece de la vista del paciente.

### 9. Detalle de una cita existente
- **Elementos:** folio, fisioterapeuta, fecha/hora, estado con semáforo, botones "Reagendar" y "Cancelar".
- **Estado "pendiente":** si la cita nació de una solicitud en revisión y aún no ha sido confirmada por el personal, aquí se ve claro ("Amarillo — en revisión, te contactaremos"), sin opción de reagendar hasta que se confirme.

### 10. Reagendamiento
- Permite seleccionar un nuevo horario reutilizando la consulta de disponibilidad, con los datos del paciente precargados.
- **Confirmación obligatoria** antes de reemplazar el horario anterior: "¿Confirmas mover tu cita del [fecha original] al [fecha nueva]? Esta acción no se puede deshacer."
- El horario anterior no se libera hasta que el nuevo quede confirmado (evita que una cancelación a medias deje al paciente sin ninguna cita).

### 11. Cancelación de cita
- Diálogo explícito antes de cancelar, con dos acciones de peso visual distinto: "Sí, cancelar mi cita" (secundario/rojo) y "Volver" (primario).
- Tras cancelar: mensaje "Cita cancelada" con opción **"Deshacer" visible por unos segundos** (control y libertad del usuario, reduce el costo del error).

### Mis citas (lista)
- Lista de tarjetas con folio, fecha y semáforo de estado; ordenadas por fecha más próxima primero.
- Estado vacío ya cubierto en pantalla 1.

### Ayuda / Contacto
- Accesible desde cualquier pantalla del flujo (ícono fijo).
- Texto directo, sin formularios: número de contacto del centro y horario de atención.

## 4. Heurísticas de Nielsen aplicadas (trazabilidad)

| Heurística | Dónde se aplica |
|---|---|
| Visibilidad del estado del sistema | Semáforo en toda pantalla con horario o cita; contador del bloqueo temporal de 5 min. |
| Coincidencia entre el sistema y el mundo real | Metáfora de agenda semanal y semáforo (Actividad 5); lenguaje "cita", no jerga técnica. |
| Control y libertad del usuario | Botón "Atrás" explícito; "Deshacer" tras cancelar; "Editar" en el resumen antes de confirmar. |
| Consistencia y estándares | Mismo componente de tarjeta de horario y mismos colores en todas las pantallas. |
| Prevención de errores | Revalidación de disponibilidad antes de confirmar; checkbox de excepción visible antes de llegar al resumen. |
| Reconocimiento antes que recuerdo | El paciente nunca debe recordar su folio de memoria para navegar; siempre disponible en "Mis citas". |
| Flexibilidad y eficiencia de uso | Salto automático de la pantalla de fisioterapeuta si solo hay una opción posible. |
| Diseño estético y minimalista | Un solo dato por fila en formularios; sin campos opcionales sin justificación. |
| Ayudar a reconocer y recuperarse de errores | Mensajes de error específicos y accionables, nunca códigos técnicos. |
| Ayuda y documentación | Acceso permanente a "Ayuda / Contacto" con una persona real detrás. |

## 5. Accesibilidad (criterios verificables, no solo "buen contraste")

- **Contraste:** mínimo 4.5:1 entre texto y fondo (equivalente a WCAG AA) en todo texto, incluidas las etiquetas dentro del semáforo.
- **El color nunca es el único portador de significado:** cada estado del semáforo lleva también una palabra ("Disponible" / "Pendiente" / "Ocupado"), pensando en daltonismo.
- **Objetivos táctiles:** mínimo 44x44px en botones y celdas de horario seleccionables — relevante porque parte de los pacientes tiene movilidad/motricidad reducida por su condición de fisioterapia.
- **Navegación por teclado:** orden de tabulación lógico (de arriba hacia abajo, de izquierda a derecha) en formularios; foco visible (contorno) en cada elemento interactivo, no solo en el hover de mouse.
- **Textos:** tamaño mínimo legible (equivalente a 16px), sin texto en mayúsculas sostenidas para párrafos largos.
- **Sin interacciones de precisión fina:** nada de arrastrar/soltar ni gestos multitáctiles; todo con tap/click simple.

## 6. Manejo de errores y casos límite

| Caso | Comportamiento esperado |
|---|---|
| No hay horarios disponibles en la semana | Estado vacío con explicación + acción de ir a la siguiente semana, nunca una grilla en blanco sin mensaje. |
| Dos pacientes seleccionan el mismo horario casi al mismo tiempo | El segundo ve el horario pasar a "Ocupado" en tiempo real y un mensaje: "Este horario ya no está disponible, elige otro." |
| El paciente cierra el flujo a medias (botón Inicio con datos sin guardar) | Confirmación: "¿Deseas salir? Perderás los datos de esta cita." antes de abandonar. |
| Falla de conexión al confirmar | Estado de error explícito con botón "Reintentar", nunca una pantalla congelada sin señal. |
| Cancelación fuera de política (ej. mismo día) | Se muestra la política de forma visible antes de confirmar la cancelación, no como sorpresa después. |
| Cita con estado "pendiente" que el paciente intenta reagendar | Bloqueado con explicación: "Esta cita aún está en revisión, espera la confirmación antes de reagendarla." |

## 7. Criterios de construcción y correspondencia con el prototipo

El prototipo utiliza componentes reutilizables para el botón primario, el botón secundario, la tarjeta de horario, la tarjeta de cita, el semáforo de estado y la barra de pasos. Esta decisión mantiene la consistencia visual entre las pantallas y permite representar cada estado mediante variantes del mismo componente.

El semáforo se presenta como un único componente con tres estados: disponible, pendiente y ocupado. Cada estado combina color y texto, de modo que la información no dependa exclusivamente de la percepción cromática.

Las interacciones del prototipo representan la selección temporal de un horario, el modal de confirmación, la confirmación de cancelación y la opción de deshacer. El enlace compartido tiene permisos de visualización para permitir la revisión del flujo navegable.
