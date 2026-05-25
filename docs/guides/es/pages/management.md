# Página Management

La página Management está centrada en el diagnóstico KNX de dispositivos e instalaciones. Dispone de cuatro pestañas: **Prog. Mode**, **Devices**, **Line Scan** e **Inspect**.

---

## Pestaña Prog. Mode

Esta pestaña permite escanear el bus en busca de dispositivos que tengan actualmente activo el modo de programación.

Pulsa el **radar FAB** para iniciar el escaneo. La aplicación escucha dispositivos en modo programación y los muestra como tarjetas. La duración del escaneo y el intervalo de ping son configurables en **Scan Settings** (icono de engranaje → Scan settings).

Cada tarjeta de dispositivo descubierta incluye dos botones:

- **Check Info** — navega a la pestaña Devices con la dirección física del dispositivo ya rellenada, lista para realizar una lectura de información del dispositivo.
- **Comm. Info** — navega a la pestaña Inspect con la dirección ya rellenada, lista para leer las tablas de comunicación del dispositivo.

Esto facilita realizar primero un escaneo y luego pasar inmediatamente a diagnósticos más avanzados en cualquier dispositivo encontrado en modo programación.

---

## Pestaña Devices

La pestaña Devices permite realizar acciones de diagnóstico sobre cualquier dirección física de dispositivo, ya sea descubierta mediante escaneo o introducida manualmente.

### Badge de Data Secure

En la parte superior de la pestaña, un badge indica si se han cargado claves de dispositivos KNX Data Secure (desde un archivo `.knxkeys` en la pestaña Security de la página Discovery). Si no se han cargado claves, el badge aparece en color ámbar. Si las claves están cargadas, el badge aparece en azul y muestra el número de dispositivos seguros. Al pulsar el badge se abre una hoja con detalles y un acceso directo para cargar un archivo `.knxkeys`.

### Entrada de Dirección

Introduce una dirección física KNX en el campo de entrada. Pulsa el **search icon** para explorar dispositivos de tu proyecto ETS cargado y seleccionar uno directamente.

### Acciones

Una vez introducida una dirección, hay disponibles cuatro acciones:

| Action | Description |
|---|---|
| **Check** | Verifica si el dispositivo está presente y responde en el bus |
| **Read Info** | Lee información detallada del dispositivo directamente desde el propio dispositivo |
| **Toggle Programming Mode** | Activa o desactiva remotamente el modo programación del dispositivo |
| **Restart** | Envía un comando de reinicio al dispositivo |

**Read Info** recupera los siguientes campos del dispositivo:
- Descriptor del dispositivo (por ejemplo, System B)
- Estado del modo programación
- Fabricante y número de pedido
- Versión de firmware
- Estado de carga y estado de ejecución
- Versión de la aplicación
- Estado de las tablas de direcciones y asociaciones
- Longitud máxima APDU
- Tipo de hardware
- Flags de error y estado del dispositivo

---

## Pestaña Line Scan

La pestaña Line Scan escanea una línea de bus KNX en busca de todos los dispositivos presentes en ella, independientemente de lo que contenga tu proyecto ETS. Esto resulta útil para verificar una instalación domótica, detectar dispositivos inesperados o trabajar con un proyecto desconocido en edificios inteligentes.

### Tarjeta Scan Settings

Configura el escaneo antes de iniciarlo:

| Setting | Description |
|---|---|
| Area and line | Área.línea KNX a escanear (por ejemplo `1.1`). Usa **Choose from project** para seleccionar una línea desde tu proyecto ETS cargado; esto también selecciona automáticamente el tipo de medio correcto. |
| Medium type | TP, IP o IoT. Necesario para que la aplicación conozca qué rango de direcciones de dispositivos debe sondear. |
| Range | Dirección inicial y final dentro de la línea (0–255). Reduce el rango para acelerar el escaneo o comprobar un segmento específico. |

Pulsa el **scan FAB** para iniciar el escaneo. El escaneo puede detenerse en cualquier momento antes de completarse.

### Resultados del Escaneo

Los dispositivos descubiertos aparecen como tarjetas. El color del borde de la tarjeta indica el tipo de dispositivo:

| Colour | Device type |
|---|---|
| Blue | Acoplador KNX |
| Red | Dispositivo de aplicación estándar |
| Green | Dispositivo KNX Secure |

Un botón **Read Device Info** aparece sobre la lista de tarjetas una vez finalizado el escaneo. Al pulsarlo se lee la información del dispositivo (fabricante, número de serie y otros detalles) para todos los dispositivos descubiertos de forma secuencial; muy útil para obtener rápidamente una visión general de una instalación domótica KNX que no hayas puesto en marcha tú mismo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-line-scan.png" width="320" alt="Line scan tab showing discovered device cards with colour-coded borders and the Read Device Info button" />
</div>

### Hoja de Detalles de la Tarjeta de Dispositivo

Pulsa cualquier tarjeta de dispositivo descubierta para abrir su hoja de detalles. Contiene:

- Una tarjeta de información del dispositivo (rellenada si se ejecutó Read Device Info)
- Las mismas cuatro acciones de diagnóstico que en la pestaña Devices: **Check**, **Read Info**, **Toggle Programming Mode**, **Restart**
- **Program Address** — abre una subpágina donde puedes introducir una nueva dirección física (o buscar una en tu proyecto) y programarla en el dispositivo utilizando uno de estos dos métodos:
  - **Via programming button** — espera hasta 20 segundos a que un dispositivo entre en modo programación y luego escribe la dirección. También comprueba conflictos de direcciones frente a la instalación real.
  - **Via serial number** — si ya has leído la información del dispositivo y dispones de su número de serie, programa la dirección sin requerir acceso físico al botón de programación.
- **Rebuild Communication** — navega a la pestaña Inspect con la dirección de este dispositivo ya rellenada.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-device-card.png" width="320" alt="Line scan device card detail sheet showing diagnostic action buttons and Program Address option" />
</div>

---

## Pestaña Inspect

La pestaña Inspect lee las tablas de comunicación de un dispositivo directamente desde su memoria. Esto reconstruye qué objetos de comunicación existen, qué flags tienen y qué direcciones de grupo están conectadas a ellos, sin necesidad de un proyecto ETS. Es la forma más eficaz de comprender un dispositivo desconocido o verificar un dispositivo en un proyecto que no hayas creado tú mismo.

### Lectura de un Dispositivo

Introduce la dirección física de un dispositivo en el campo de entrada y pulsa **Read**. Una barra de progreso muestra qué operación está en curso. Tras completarse, aparece una tarjeta de sesión para el dispositivo.

El color del borde de la tarjeta indica éxito o fallo. Cada tarjeta muestra:
- Dirección física del dispositivo
- Descriptor del dispositivo (por ejemplo, System B, acoplador KNX)
- Si se ha leído la información completa del dispositivo (muestra fabricante y número de pedido si es así)

Un botón **Read Full Info** en cada tarjeta ejecuta una lectura adicional de información del dispositivo si deseas obtener todos los detalles sin ralentizar la reconstrucción inicial de tablas.

Las tarjetas de sesión son **persistentes** — permanecen incluso después de reiniciar la aplicación. Utiliza el botón **Clear** sobre la lista de tarjetas para eliminar todas las sesiones cuando hayas terminado.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect.png" width="320" alt="Inspect tab showing multiple session cards for different devices" />
</div>

### Página de Detalles de Sesión

Pulsa cualquier tarjeta de sesión para abrir su página completa de detalles. La barra superior muestra la dirección del dispositivo y el descriptor, un botón **reload** para volver a ejecutar la reconstrucción y un botón **share** para exportar y compartir un informe PDF de esta sesión.

La página de detalles dispone de tres pestañas:

#### Associations

Lista todos los objetos de comunicación leídos desde la memoria del dispositivo que tienen direcciones de grupo conectadas:

| Column | Description |
|---|---|
| Number | Índice del objeto de comunicación |
| Flags | R (Read), W (Write), C (Communication), T (Transmit), U (Update), I (Read-on-Init) |
| Size | Tamaño del objeto (1 bit, 1 byte, 2 bytes, etc.) |
| Group addresses | Direcciones conectadas a este objeto |

Cada dirección de grupo es pulsable. Como el tipo de punto de datos no puede conocerse únicamente desde la memoria, se presenta una entrada de valor RAW en hex o decimal para enviar comandos de prueba.

Los botones **Export CSV** y **Export TXT** exportan la lista de asociaciones solo para este dispositivo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect-associations.png" width="320" alt="Associations tab showing communication objects with flags, size, and linked group addresses" />
</div>

#### Device Info

Muestra la tarjeta completa de información del dispositivo (los mismos campos que la acción Read Info de la pestaña Devices). Incluye un botón **Read Info** si todavía no se ha leído la información y un botón **Copy All** que copia todos los campos al portapapeles para compartirlos con compañeros o integradores de sistemas KNX.

#### Addresses

Una tabla de todas las direcciones de grupo leídas desde la tabla de direcciones del dispositivo en memoria, con columnas para índice, formato de 3 niveles, formato de 2 niveles y valor hex. Cada fila puede copiarse individualmente. Los botones **Copy All** y **Export CSV** están disponibles sobre la tabla.

---

## Menú Tune

El icono tune en la barra superior proporciona dos acciones de exportación para el resultado más reciente del line scan:

- **Export as text** — exporta un informe TXT con la marca temporal del escaneo, gateway utilizado, área/línea escaneada, medio y una lista de dispositivos descubiertos con su información
- **Export as PDF** — el mismo contenido en formato PDF
