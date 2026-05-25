# Shark Hunts Page

La pantalla **Shark Hunts page** es el lugar donde puede crear, gestionar y ejecutar **shark hunts**, conjuntos reutilizables de acciones de envío KNX y filtros de monitorización guardados como archivos JSON portátiles esenciales para el **control KNX**. Un "hunt" le ofrece una página dedicada con acciones de un solo toque, filtros preconfigurados y una pasarela (gateway) integrada opcional, lista para compartir con colegas o clientes en cualquier **instalación domótica**.

Para conocer el concepto subyacente, consulte [Shark Hunts](../concepts/shark-hunts.md).

---

## Main Page Layout

Debajo de la barra superior hay una fila de filtro de texto. Escriba para filtrar las tarjetas de hunts por nombre. El **star icon** a la derecha de la fila filtra inmediatamente para mostrar solo los hunts que ha marcado como favoritos.

La barra superior contiene:

- **Help button** — abre una página de referencia dentro de la aplicación que cubre el concepto de Shark Hunt, los tipos de acciones y ejemplos
- **Tune icon** — dos acciones:
  - **Export Hunts** — exporta todos los hunts existentes como un único archivo JSON
  - **Import Hunts** — importa un archivo JSON que contiene uno o más hunts

### Creating a Hunt

Toque el **+ FAB** para abrir el asistente de creación de cinco pasos. Consulte [Create a Shark Hunt](../how-to/create-shark-hunt.md) para ver una guía completa que facilite la **domótica KNX** en **edificios inteligentes**.

### Hunt Cards

Cada hunt creado aparece como una tarjeta. El color del borde superior de la tarjeta indica su tipo:

| Color del borde | Tipo de hunt |
|---|---|
| Verde | Solo acciones de envío (Send actions) |
| Azul | Solo acciones de monitorización (Monitor actions) |
| Rojo | Tanto acciones de envío como de monitorización |

Cada tarjeta muestra el nombre del hunt, la descripción (si la hay) y la etiqueta de tipo. También cuenta con:

- **Star icon** — marcar o desmarcar como favorito
- **Three-dot menu** — Edit, Export (un solo JSON), Share, Delete e Info
  - **Info** abre una hoja con el nombre, tipo, estado de favorito, recuento y nombres de acciones, y las marcas de tiempo de creación/modificación

Al mantener presionada cualquier tarjeta se ingresa al modo de selección múltiple, lo que le permite copiar, exportar o eliminar varios hunts a la vez.

Las tarjetas de hunts son persistentes y sobreviven a los reinicios de la aplicación.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-main.png" width="320" alt="Pantalla principal de Shark Hunts que muestra las tarjetas de hunts con bordes superiores codificados por colores y la fila de filtros" />
</div>

---

## Hunt Detail Page

Al tocar una tarjeta de hunt se abre su página dedicada. La barra superior muestra un botón de retroceso y una entrada de filtro para buscar dentro de las tarjetas de acción en esta página.

### Badge Row

| Badge | Descripción |
|---|---|
| **Hunt name** | Al tocarlo se abre la hoja de información del hunt (nombre, tipo, favorito, recuento de acciones, marcas de tiempo) |
| **Connection status** | Rojo = desconectado, Verde = conectado. Al tocarlo se conecta o desconecta de la pasarela (gateway) |
| **ETS Project** | Muestra si hay un proyecto **ETS** cargado. Al tocarlo se abre una hoja con los detalles del proyecto (nombre, formato de dirección de grupo [GA], fechas) y un botón para cargar o descargar el proyecto |
| **Data Secure** | Muestra el estado del remitente KNX Data Secure. Gris = no hay direcciones de grupo (GAs) con Data Secure cargadas; ámbar = GAs presentes pero sin remitentes configurados (toque para configurar); verde = remitentes configurados (toque para revisar) |
| **Gateway** | Muestra la dirección IP de la pasarela (gateway) seleccionada. Azul = seleccionada, gris = ninguna seleccionada, verde = seleccionada y conectada. Al tocarlo se abre una hoja con los detalles de la pasarela y un botón para limpiar la selección (cuando no se está monitorizando) |

### Connecting

Toque el **green connect FAB** para conectarse a la pasarela configurada. Si no se selecciona ninguna pasarela (gateway), una ventana emergente enumera las opciones disponibles, incluida cualquier pasarela integrada en el hunt durante la creación, además de otras pasarelas descubiertas y configuradas manualmente. Una vez conectado, el FAB se vuelve rojo con un icono de parada para desconectarse.

Todas las tarjetas de acción se muestran atenuadas y no son interactivas hasta que se establece la conexión.

---

## Send Actions Section

Las tarjetas de acciones de envío están agrupadas en la sección superior de la página del hunt. Al tocar una tarjeta, se ejecuta inmediatamente:

- **Fixed action** — envía el valor preconfigurado sin ninguna confirmación o aviso
- **Multiple / Sequence action** — envía todos los comandos en secuencia, con los retrasos configurados entre ellos
- **Variable action** — abre una hoja inferior con una interfaz de usuario de entrada adecuada para el **DPT** (por ejemplo, controles deslizantes de color para RGB, un control deslizante de porcentaje para DPT 5.001). Confirme con el botón de envío.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Página de detalles del hunt que muestra las tarjetas de acciones de envío en la sección superior y las tarjetas de acciones de monitorización abajo" />
</div>

---

## Monitor Actions Section

Las tarjetas de acciones de monitorización están agrupadas debajo de las de envío. Al tocar una tarjeta se abre el **Shark Hunt Monitor** para esa acción: una sesión de monitorización con los filtros de la acción aplicados de inmediato para un óptimo **diagnóstico KNX**.

### Shark Hunt Monitor

La página **Shark Hunt Monitor** es similar a la [Monitor page](monitor.md) principal, pero acotada al filtro de la acción activa. La barra superior muestra el nombre del hunt como título y el nombre de la acción de monitorización como subtítulo, además de un botón **save/export** (activo cuando hay telegramas presentes).

#### Badge Row

| Badge | Descripción |
|---|---|
| **Send** | Abre una hoja inferior para redactar y enviar un comando. También muestra fichas (chips) de envío rápido para comandos recientes; mantenga presionada una ficha para volver a abrir el redactor con los campos completados previamente |
| **Filter details** | Muestra las condiciones del filtro actualmente activo |
| **Clear** | Borra todos los **telegramas** de la lista |
| **Data Secure** | Igual que el badge Data Secure de la página de detalles del hunt |
| **View** | Orden de clasificación (más nuevos primero / más antiguos primero) y formato de dirección de grupo. Afecta a los nuevos telegramas entrantes |
| **Statistics** | Total de telegramas, tasa de telegramas/seg, direcciones de grupo principales, dispositivos de origen principales y tipos de telegramas principales |
| **Gateway** | Igual que el badge de gateway de la página de detalles del hunt |

Los **monitor FABs** funcionan de la siguiente manera:
- Grande FAB — verde/start para comenzar la monitorización, rojo/stop para finalizar
- Pequeño FAB encima — abre una hoja que enumera todas las acciones de monitorización en este hunt, para que pueda cambiar de filtro sin salir de la página. La acción actualmente activa se muestra con un punto verde

#### Telegram List

Cada fila de telegrama muestra:
- Dirección física del remitente → dirección de grupo de destino
- Nombre de la dirección de grupo | valor | valor hex en formato RAW (el nombre y el valor requieren un proyecto **ETS** cargado)
- Marca de tiempo en formato HH:MM:SS.ms

Al tocar una fila se abre la hoja de detalles del telegrama con todos los campos (hora, origen, destino, nombre, valor, carga útil RAW) y dos botones de acción: **Read** (envía un comando de lectura a la dirección de grupo) y **Write** (abre el redactor de comandos precompletado con la dirección y el **DPT**). Un tercer botón, **Plot**, abre una vista de gráfico con dos pestañas: un gráfico de series temporales del valor de la dirección de grupo y un gráfico de barras de las direcciones físicas de origen.

#### Export

La hoja de exportación le permite dar un nombre al archivo (precompletado con una marca de tiempo), elegir qué columnas incluir (ID, hora, origen, destino, nombre, tipo, valor, raw), establecer cuántos telegramas exportar, alternar los encabezados de las columnas y elegir un delimitador (coma, tabulación o punto y coma).
