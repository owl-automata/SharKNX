# Cómo exportar telegramas

SharKNX permite exportar los telegramas que se encuentran actualmente en la lista del monitor a un archivo. Puedes elegir qué columnas incluir, la cantidad de telegramas, el estilo de los encabezados de columna y el formato del delimitador. Los archivos exportados se pueden guardar localmente o compartir directamente desde la aplicación.

---

## Desde la página Monitor

1. Inicia una sesión de monitorización y deja que se acumulen los telegramas, o detén el monitor cuando hayas capturado el tráfico de red necesario.
2. Toca el **icono de exportación** (en la parte superior derecha de la fila de la barra de filtros) para abrir el panel de exportación (*export sheet*).
3. Configura la exportación:

   | Opción | Descripción |
   |---|---|
   | **File name** | Autocompletado con una marca de tiempo. Edítalo para darle un nombre significativo al archivo. |
   | **Columns** | Marca las columnas que deseas incluir: ID, Time, Source, Destination, Name\*, Type, Value\*, Raw (\*requieren un proyecto ETS cargado) |
   | **Number of telegrams** | Cuántos telegramas exportar (contados a partir del más reciente). Utilízalo para limitar un búfer grande a las últimas N entradas. |
   | **Include column headers** | Actívalo para incluir una fila de encabezado en la parte superior del archivo CSV. |
   | **Delimiter** | Comma (Coma - por defecto), Tab (Tabulador) o Semicolon (Punto y coma). |

4. Toca **Save** para guardar el archivo en tu dispositivo, o **Share** para abrir el panel de compartición del sistema y enviarlo directamente por correo electrónico, almacenamiento en la nube u otra aplicación.

---

## Desde el monitor de una Shark Hunt

El mismo panel de exportación está disponible dentro de una sesión de monitorización en una Shark Hunt. Toca el **botón de guardar/exportar** en la barra superior (se activa cuando hay telegramas presentes). Se aplican exactamente las mismas opciones descivos anteriormente.

---

## Notas importantes

- Las columnas **Name** (Nombre) y **Value** (Valor) solo contienen información útil cuando hay un proyecto ETS cargado en la aplicación. Sin un proyecto, estas columnas aparecerán vacías para la mayoría de los telegramas.
- La columna **Raw** siempre está disponible y contiene la carga útil en hexadecimal sin procesar (*hex payload*). Este es el valor real (el *ground truth*) que la app traduce a un formato legible por humanos cuando se dispone del proyecto.
- La exportación captura lo que esté almacenado en ese momento en el búfer de telegramas. Si el búfer ha alcanzado su límite (por defecto 2000, configurable en **Settings → Monitor**), los telegramas más antiguos ya se habrán sobrescrito. Realiza la exportación antes de que el búfer se llene si necesitas una captura extensa de tu instalación KNX.
- Los archivos exportados se pueden volver a importar en el monitor para su posterior análisis y diagnóstico de domótica. Desde el **menú de ajustes (icono de sintonización/rueda) en Monitor**, utiliza **Import CSV** para cargar un archivo exportado previamente de vuelta en la lista de telegramas.
