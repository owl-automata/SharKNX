# Página Monitor

La página Monitor proporciona una sesión de monitorización en vivo del bus KNX. Los telegramas entrantes se capturan en tiempo real y se muestran en una lista desplazable. Puedes filtrar, inspeccionar, representar gráficamente y exportar telegramas, además de enviar comandos al bus sin abandonar la página.

---

## Inicio y Detención

Pulsa el **start FAB** verde para iniciar una sesión de monitorización.

- Si no hay ningún gateway seleccionado, aparece un selector con tus gateways descubiertos y guardados. Selecciona uno para continuar.
- La aplicación se conecta al gateway y comienza inmediatamente a capturar telegramas.
- El FAB cambia a un **send FAB** rojo mientras el monitor está en ejecución (consulta [Sending Commands](#sending-commands)).

Pulsa el badge **Start/Stop** en la fila de badges (ver más abajo) para detener el monitor. La lista de telegramas permanece visible después de detenerlo; no se borra hasta que la limpies explícitamente.

---

## Fila de Barra de Filtros

La fila de barra de filtros está fijada sobre la lista de telegramas y siempre es visible.

**Text filter bar** — escribe cualquier texto para filtrar la lista visible de telegramas. Coincide con nombres de direcciones de grupo, valores y direcciones físicas. La lista subyacente no se modifica; elimina el filtro para volver a ver todos los telegramas capturados.

**Search filter icon** — abre una hoja inferior con dos pestañas: una lista todas las direcciones de grupo de tu proyecto ETS cargado y la otra todos los dispositivos. Pulsa cualquier entrada para aplicarla inmediatamente como filtro activo. Resulta útil para aislar rápidamente una dirección de grupo o dispositivo específico sin escribir manualmente.

**Always-on-top button** — cuando está habilitado (por defecto), la lista se desplaza automáticamente hasta el telegrama más reciente cada vez que llega uno nuevo. La vista detecta automáticamente cuando estás desplazándote manualmente y pausa el desplazamiento automático hasta que vuelvas arriba. Pulsar el botón mientras está deshabilitado mueve inmediatamente la vista al inicio.

**Export button** — abre la hoja inferior de exportación. Consulta [Exporting Telegrams](#exporting-telegrams).

---

## Fila de Badges

Una fila desplazable de badges está fijada debajo de la barra de filtros. Cada badge es pulsable.

### Start / Stop
Inicia o detiene la sesión de monitorización. Tiene la misma función que el start FAB antes de que el monitor esté en ejecución.

### Clear
Borra todos los telegramas de la lista. La sesión de monitorización continúa activa si está en ejecución.

### ETS Project
Muestra si hay un proyecto ETS cargado. Al pulsarlo se abre una hoja con detalles del proyecto (nombre, formato de direcciones de grupo, fechas de creación y modificación) y un botón para descargar el proyecto. Si no hay ningún proyecto cargado, la hoja incluye un botón **Load Project** que abre el mismo selector de archivos que la página Project.

### Data Secure
Refleja el estado de KNX Data Secure para la sesión actual:

| Badge state | Meaning |
|---|---|
| Gray | No hay direcciones de grupo data secure en el proyecto cargado |
| Amber | Hay direcciones data secure presentes, pero los remitentes no están configurados |
| Green | Hay direcciones data secure presentes y remitentes configurados |

Al pulsar un badge ámbar se abre una hoja con un botón para navegar a la página de configuración de Data Secure Senders. Consulta [KNX Data Secure](../concepts/knx-data-secure.md).

### Telegrams
Muestra el número actual de telegramas. Al pulsarlo se abre una hoja con:
- **Clear filter** — elimina cualquier filtro de texto o búsqueda activo (solo visible cuando hay un filtro activo)
- **Clear telegrams** — elimina todos los telegramas capturados
- **Statistics** — abre una vista de estadísticas que muestra:
  - Número total de telegramas
  - Tasa de telegramas/segundo (calculada desde el primer hasta el último timestamp)
  - Principales direcciones de grupo por porcentaje del total
  - Principales direcciones físicas emisoras por porcentaje
  - Principales tipos de telegrama (write, read, response, etc.) por porcentaje

### View
Abre las opciones de visualización para la lista de telegramas:
- **Sort order** — más recientes primero (por defecto) o más antiguos primero
- **Address level format** — cómo se muestran las direcciones de grupo (3 niveles, 2 niveles o libre). Por defecto utiliza el formato del proyecto ETS cargado. Los cambios afectan únicamente a los nuevos telegramas entrantes, no a los ya visibles.
- **View Group** — navega a una segunda página de hoja donde puedes filtrar la lista visible por dirección de grupo, dirección física, tipo de telegrama o prioridad. Seleccionar una entrada muestra únicamente los telegramas coincidentes.

### Gateway
Muestra la dirección IP del gateway seleccionado. El color indica el estado de conexión:

| Colour | State |
|---|---|
| Gray | No hay gateway seleccionado |
| Blue | Gateway seleccionado, no conectado |
| Green | Seleccionado y conectado |

Al pulsarlo se abre una hoja con detalles del gateway y un botón **Clear selection** (disponible solo cuando el monitor está detenido).

---

## Lista de Telegramas

Cada fila de la lista muestra:
- **Dirección física emisora → dirección de grupo destino**
- **Nombre de la dirección de grupo** *(requiere proyecto ETS)* | **valor decodificado** *(requiere proyecto ETS)* | **payload RAW en hex*
- **Timestamp** en formato `HH:MM:SS.ms`

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-active.png" width="320" alt="Monitor page with live telegrams in the list view" />
</div>

### Hoja de Detalle del Telegrama

Pulsa cualquier fila para abrir la hoja de detalles de ese telegrama. Muestra:

- Timestamp
- Dirección física de origen
- Dirección de grupo de destino
- Nombre de la dirección de grupo *(si hay un proyecto ETS cargado)*
- Valor decodificado *(si hay un proyecto ETS cargado)*
- Payload RAW en hex

Hay disponibles dos botones de acción:
- **Read** — envía inmediatamente un comando de lectura a la dirección de grupo del telegrama
- **Write** — abre el compositor de comandos con la dirección de grupo y el tipo de punto de datos ya rellenados; introduce un valor y envíalo

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-telegram-detail.png" width="320" alt="Telegram detail sheet showing time, source, destination, value, and Read/Write/Plot buttons" />
</div>

### Plot

Un botón **Plot** en la hoja de detalles abre una vista de gráficos de dos pestañas para la dirección de grupo seleccionada:

- **Value tab** — gráfico de series temporales de todos los valores capturados para esta dirección. Pellizca para hacer zoom, desplázate horizontalmente y pulsa un punto para ver su valor exacto y timestamp.
- **Sources tab** — gráfico de barras de las direcciones físicas emisoras que han transmitido esta dirección de grupo, útil para identificar emisores inesperados o realizar diagnóstico KNX de "ruido" en el bus.

Una tarjeta de información muestra el rango temporal cubierto por los datos del gráfico.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-plot.png" width="320" alt="Plot view showing a time series chart of a group address value over time" />
</div>

---

## Sending Commands

Mientras el monitor está en ejecución, el FAB se convierte en un **send FAB** rojo. Al pulsarlo se abre una hoja inferior con:

- **New Command** — abre el compositor de comandos. Introduce una dirección de grupo (o búscala desde el proyecto ETS cargado), selecciona write o read, elige el tipo y subtipo de punto de datos, introduce un valor y pulsa **Send**. El comando enviado aparece inmediatamente en la lista de telegramas.
- **Quick command chips** — debajo del botón de nuevo comando aparecen chips de comandos enviados recientemente. Pulsa un chip para reenviar instantáneamente el mismo comando. Mantén pulsado un chip para volver a abrir el compositor con los campos del comando ya rellenados y así poder ajustar el valor antes de enviarlo.

---

## Exporting Telegrams

La hoja inferior de exportación (abierta desde el export button de la fila de barra de filtros o desde el menú tune) permite guardar o compartir la lista actual de telegramas como un archivo CSV.

Opciones disponibles:

| Option | Description |
|---|---|
| Filename | Editable, rellenado automáticamente con un timestamp |
| Columns | Casillas de selección para id, time, source, destination, name, type, value, raw |
| Telegram count | Elige cuántos telegramas exportar (por ejemplo, los últimos 100 de 5000) |
| Include headers | Activa o desactiva la fila de encabezados de columna en el CSV |
| Delimiter | Coma (por defecto), tabulación o punto y coma |

**Save** escribe el archivo en el almacenamiento del dispositivo. **Share** abre la hoja de compartición del sistema para enviarlo directamente a una aplicación de mensajería, almacenamiento en la nube o correo electrónico.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-export.png" width="320" alt="Export bottom sheet showing filename input, column selection tick boxes, and Save/Share buttons" />
</div>

Consulta [Export Formats](../reference/export-format.md) para conocer la estructura completa del archivo CSV.

---

## Menú Tune

El icono tune en la barra superior abre acciones adicionales para la página Monitor:

**Import SharKNX CSV** — carga en la lista de telegramas un archivo CSV exportado previamente desde SharKNX. Los telegramas importados reemplazan la lista actual. El archivo debe coincidir con el formato de exportación de SharKNX.

**Export telegrams** — igual que el export button de la fila de barra de filtros.

**Import from ETS XML** — carga un archivo de exportación de telegramas de la herramienta de software ETS. Resulta útil para visualizar y analizar una grabación realizada en ETS desde tu dispositivo móvil o compartirla con compañeros. Reemplaza la lista actual de telegramas.

**Apply project data** — después de cargar o actualizar un proyecto ETS, aplica retroactivamente los nombres de direcciones de grupo y tipos de punto de datos del proyecto a todos los telegramas actualmente presentes en la lista. El monitor debe estar detenido antes de ejecutar esta acción. Úsalo cuando cargues un proyecto después de haber capturado telegramas o cuando recargues un proyecto actualizado y quieras reflejar los nuevos nombres en los datos capturados existentes.
