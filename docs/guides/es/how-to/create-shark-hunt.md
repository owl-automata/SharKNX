# Cómo crear una Shark Hunt

Una Shark Hunt es un conjunto reutilizable de acciones de envío y filtros de monitorización guardados en un archivo portátil. Esta guía te guiará a través del asistente de creación de cinco pasos y explica cómo configurar cada uno de los seis tipos de acciones disponibles para el control y diagnóstico KNX.

Para obtener una visión general de qué son las Shark Hunts y cómo funciona la página principal, consulta [Shark Hunts](../concepts/shark-hunts.md).

> La aplicación admite hasta **25 hunts**. Cada una de ellas permite configurar hasta **25 acciones**.

---

## El asistente de creación (Wizard)

En la página principal de Shark Hunts, toca el **botón flotante (FAB) +** para abrir el asistente.

Cada paso del asistente cuenta con:
- Un **botón X** (arriba a la izquierda) para cerrar: la app te avisará si hay cambios sin guardar.
- Botones **Back / Next** (Atrás / Siguiente) en la parte inferior para navegar entre los pasos.
- Un **botón Save** (Guardar) (arriba a la derecha) que aparece en cuanto realizas cualquier cambio, lo que te permite guardar el progreso y salir para terminarlo más tarde.

---

### Paso 1 — Nombre y descripción

Introduce un **nombre** para la Shark Hunt (obligatorio) y una **descripción** opcional. Activa la opción **Mark as favourite** (Marcar como favorito) si deseas que aparezca en primer lugar al filtrar por estrella en la página principal.

---

### Paso 2 — Proyecto ETS

Elige si esta Shark Hunt utilizará un proyecto de ETS (el software estándar de domótica KNX):

| Opción | Cuándo usarla |
|---|---|
| **Use loaded ETS project** | Si ya hay un proyecto cargado: la Shark Hunt utilizará sus direcciones de grupo, dispositivos y la estructura del edificio para crear acciones y filtros de monitorización |
| **Load a project** | Si aún no hay ningún proyecto cargado: abre el selector de archivos para que puedas cargar uno en este momento |
| **Manual input** | Si no tienes o no necesitas un proyecto: las direcciones de grupo deberán escribirse manualmente al crear las acciones |

> Los tipos de acción **Monitor Space** y **Monitor Device** requieren obligatoriamente un proyecto ETS. Si omites la selección del proyecto en este paso, estos dos tipos de acción no estarán disponibles en el Paso 3.

---

### Paso 3 — Acciones

Aquí es donde construyes el contenido de tu Shark Hunt. Toca en **Add action** y elige un tipo de acción de la lista. Consulta la sección [Tipos de acciones](#tipos-de-acciones) más abajo para conocer todos los detalles de cada tipo.

Las acciones creadas aparecerán en forma de tarjetas. Cada tarjeta incluye:
- **Edit** — Reabrir la configuración de la acción.
- **Copy** — Duplicar la acción (muy útil para acciones similares con pequeñas diferencias).
- **Delete** — Eliminar la acción.

Repite el proceso hasta que tengas todas las acciones que necesites para tu diagnóstico KNX.

---

### Paso 4 — Gateway (Opcional)

De forma opcional, puedes incrustar la configuración de un Gateway KNX en la Shark Hunt. Esto permite que el destinatario de una *hunt* compartida se conecte directamente sin necesidad de buscar o configurar el Gateway por sí mismo (ideal para compartir con usuarios no expertos o clientes para soporte técnico remoto).

Selecciona uno de los Gateways ya descubiertos o toca en **Configure manually** para introducir una dirección IP y un puerto de forma manual. Este paso se puede omitir por completo si no necesitas un Gateway incrustado.

---

### Paso 5 — Revisar y crear

Un resumen de todas tus selecciones. Revísalo y toca en **Create** para finalizar. La Shark Hunt aparecerá en la página principal en forma de tarjeta.

---

## Tipos de acciones

Cada página de creación de acciones requiere un **nombre de acción** (obligatorio) y una **descripción** opcional. El **botón flotante (FAB) de confirmación (check/tick)** se activará una vez que se hayan completado todos los campos obligatorios; al tocarlo, se guardará y creará la acción.

---

### Send Fixed (Envío de valor fijo)

Envía un valor fijo a una dirección de grupo específica cada vez que se toca la acción.

1. Introduce la dirección de grupo o toca el **icono de búsqueda** para seleccionar una del proyecto ETS cargado (esto autorrellenará el DPT correspondiente).
2. Elige entre **Write** (Escritura) o **Read** (Lectura).
3. Selecciona el tipo y subtipo de **DPT** (Datapoint Type).
4. Para acciones de tipo *Write*: introduce el valor a enviar (por ejemplo: On, 75%, 21.5°C, Escena 3).
5. Toca el **botón FAB de confirmación** para guardar.

**Ejemplos:** Encender/apagar una luz, establecer la consigna de un termostato, ejecutar una escena o probar la posición de una persiana en tu instalación KNX.

---

### Send Multiple / Sequence (Envío múltiple / Secuencia)

Envía una lista de comandos fijos en secuencia, con la posibilidad de añadir retardos entre ellos.

1. Toca el **botón +** para añadir el primer comando (se abrirá el compositor de comandos). Introduce la dirección de grupo, el DPT, si es lectura/escritura y el valor; luego toca el botón de confirmación para añadirlo.
2. Toca **+** de nuevo para añadir más comandos (hasta un máximo de **15**).
3. Cada comando aparece como una tarjeta desplegable que muestra su DPT y valor.
4. Para añadir un retraso antes de un comando: toca el subtítulo **"Immediate"** en la tarjeta e introduce el tiempo de espera en segundos (máximo **10 s**). El siguiente comando esperará ese tiempo antes de ejecutarse.
5. Para reordenar: toca el **icono de arrastrar de seis puntos** en cualquier tarjeta y muévela a la posición deseada.
6. Toca el **botón FAB de confirmación** para guardar la acción.

**Ejemplo:** Activar escena → esperar 2 s → leer estado de la iluminación → esperar 1 s → enviar confirmación.

---

### Send Variable (Envío de valor variable)

Envía un valor que tú elijas en tiempo de ejecución a una o varias direcciones de grupo. Es muy útil cuando necesitas probar diferentes valores en la misma dirección o realizar un envío masivo a varias direcciones relacionadas a la vez.

1. Introduce una dirección de grupo en el campo de entrada y toca **Add**. Repite el proceso para cada dirección de destino (hasta un máximo de **15**).
   - Utiliza la **búsqueda del proyecto** para seleccionar múltiples direcciones de grupo a la vez desde tu proyecto ETS cargado.
2. Todas las direcciones añadidas deben compartir el mismo DPT. Si hay discrepancias, se resaltarán en las tarjetas de dirección, pero no bloquearán la creación (solo ten en cuenta que es posible que el dispositivo KNX no responda como se espera).
3. Toca el **botón FAB de confirmación** para guardar.

Cuando ejecutes esta acción en la página de la Shark Hunt, se abrirá un panel inferior (*bottom sheet*) con un campo de entrada adecuado para el DPT configurado. Introduce el valor y confirma para enviarlo a todas las direcciones de destino.

**Ejemplos:** Seleccionar todas las direcciones de grupo de consigna de termostatos de una planta y enviar 21 °C con un solo toque para verificar que cada zona de climatización responde correctamente. O seleccionar todas las direcciones de regulación de un canal de dimmer en una sala e ir variando los porcentajes de brillo para localizar cuál está causando parpadeos en las luminarias.

---

### Custom Monitor (Monitor personalizado)

Crea un filtro avanzado para una sesión de monitorización utilizando una o más condiciones combinadas con lógica AND / OR.

1. Toca el **botón +** para añadir una condición. Se pueden añadir hasta **10 condiciones**.
2. Elige el tipo de condición:

   | Condición | Qué filtra |
   |---|---|
   | **Group address** | Muestra solo los telegramas hacia/desde direcciones de grupo específicas. Introduce las direcciones manualmente o selecciónalas desde el proyecto. Admite comodines (`1/*/*`, `1/*/0`). Activa **Exclude** para invertir el filtro (mostrar todo excepto esas direcciones). |
   | **Device address** | Muestra solo los telegramas procedentes de direcciones físicas (direcciones de dispositivo) específicas. Entrada manual o búsqueda en el proyecto. Admite comodines (`1.*.*`). Activa **Exclude** para invertirlo. |
   | **Telegram type** | Filtra por tipo de APCI: Write (Escritura), Read (Lectura), Response (Respuesta) o cualquier combinación de ellos. |
   | **Text search** | Muestra solo los telegramas cuyo nombre o descripción de la dirección de grupo contenga el texto buscado. Requiere un proyecto ETS cargado. |
   | **Timestamp** | Muestra telegramas antes, después o entre horas específicas. Ideal para comprobar automatizaciones horarias. |

3. Después de añadir las condiciones, establece el **operador lógico** entre ellas: **AND** (deben cumplirse todas las condiciones) u **OR** (basta con que se cumpla una de las condiciones).
4. Toca el **botón FAB de confirmación** para guardar.

**Ejemplos:**
- *Aislar un dispositivo sospechoso:* Añade una condición de *Device Address* para el emisor sospechoso Y una condición de *Group Address* para el rango de direcciones afectado. Solo aparecerán los telegramas de ese dispositivo hacia esas direcciones, filtrando todo lo demás.
- *Verificar una automatización matutina:* Añade una condición de *Timestamp* (después de las 07:00) Y una condición de *Telegram Type* (solo Write). Ejecuta el monitor a la mañana siguiente y confirma que el programador envió los comandos correctos a la hora exacta.
- *Monitorizar todo excepto tu propio tráfico de pruebas:* Añade una condición de *Device Address* con la opción **Exclude** activada para la dirección física de tu portátil o smartphone, de modo que solo veas el tráfico real de la instalación KNX mientras realizas los tests.

---

### Monitor Space (Monitorear espacio físico)

Crea rápidamente un filtro de monitorización delimitado a un espacio físico de la estructura del edificio de tu proyecto ETS. Requiere un proyecto ETS cargado (configurado en el Paso 2).

1. Elige qué deseas monitorizar:
   - **Group addresses** — Monitoriza todas las direcciones de grupo asignadas a los dispositivos del espacio seleccionado.
   - **Device senders** — Monitoriza todas las direcciones físicas de los dispositivos ubicados en el espacio seleccionado.
2. Toca en **Select space** — La estructura de tu edificio del ETS aparecerá en un panel desplegable. Selecciona una planta, una habitación o cualquier ubicación (por ejemplo: Cocina, Salón).
3. Toca el **botón FAB de confirmación** para guardar.

> Se pueden capturar hasta **750 direcciones** a partir de la selección de un solo espacio. Los espacios muy grandes con muchos dispositivos integrados pueden acercarse a este límite.

---

### Monitor Device (Monitorear dispositivo)

Crea un filtro de monitorización acotado a uno o varios dispositivos específicos de tu proyecto ETS. Requiere un proyecto ETS cargado (configurado en el Paso 2).

1. Toca en **Select devices** — Aparecerá la lista de dispositivos de tu proyecto. Selecciona uno o varios dispositivos.
2. El filtro monitorizará todas las direcciones de grupo que estén vinculadas a los dispositivos seleccionados.
3. Toca el **botón FAB de confirmación** para guardar.

> Se aplica el mismo límite de **750 direcciones**. Es una herramienta excelente para probar la comunicación entre dos dispositivos específicos o verificar todas las salidas de un actuador KNX.

---

## Editar una Shark Hunt existente

Desde la página principal, toca el **menú de tres puntos** en cualquier tarjeta de Shark Hunt y selecciona **Edit**. Esto volverá a abrir el asistente con todos los datos existentes. Podrás cambiar el nombre, añadir o eliminar acciones, modificar el Gateway o actualizar cualquier otro ajuste.

---

## Compartir una Shark Hunt

Desde el menú de tres puntos, toca en **Share** para exportar la Shark Hunt como un archivo JSON a través de cualquier aplicación (correo electrónico, mensajería, almacenamiento en la nube). El destinatario podrá importarla usando el **icono de ajustes (tuerca/sintonización) → Import Hunts** en su propia página de Shark Hunts. Un único archivo exportado puede contener una o varias de estas configuraciones de control KNX.
