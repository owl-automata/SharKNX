# Cómo inspeccionar los objetos de comunicación de un dispositivo

La pestaña **Inspect** de la página Management lee las tablas de comunicación de un dispositivo directamente desde su memoria y reconstruye qué objetos de comunicación existen, qué flags tienen asignados y qué direcciones de grupo están vinculadas a ellos, todo esto sin necesidad de disponer de un proyecto ETS. Es el método más fiable para auditar y comprender un dispositivo desconocido o mal documentado en una instalación de domótica KNX.

---

## Requisitos previos

- Estar conectado a un Gateway KNX (consulta [Conectarse a un Gateway](connect-to-gateway.md)).
- Conocer la dirección física (individual) del dispositivo que deseas inspeccionar.

---

## Pasos a seguir

1. Ve a **Management → pestaña Inspect**.
2. Introduce la dirección física del dispositivo en el campo de entrada.
   - También puedes acceder a esta pestaña con la dirección ya cumplimentada desde la pestaña **Prog. Mode** (tocando en **Comm. Info** dentro de una tarjeta), desde la tarjeta de un dispositivo en un **Line Scan** (tocando en **Rebuild Communication**), o desde cualquier panel de detalles de dispositivo.
3. Toca en **Read**. Una barra de progreso te indicará la operación que se está ejecutando en cada momento (tabla de direcciones, tabla de asociación u objetos de comunicación).
4. Aparecerá una tarjeta de sesión para el dispositivo. El color del borde indicará si la lectura fue correcta (verde) o si se produjo un fallo (rojo).

---

## Leer la información completa del dispositivo (Full Info)

La lectura de la tabla de comunicación no incluye por defecto los datos detallados del dispositivo (fabricante, firmware, etc.). Toca en **Read Full Info** en la tarjeta de sesión para recuperar esos detalles de forma independiente.

---

## Ver los detalles de la sesión

Toca la tarjeta de sesión para abrir su página completa de detalles. La barra superior cuenta con un botón **reload** (recargar) para volver a ejecutar la lectura, y un botón **share** (compartir) para exportar y compartir un informe en formato PDF de esta sesión de diagnóstico KNX.

La página de detalles se divide en tres pestañas:

### Associations (Asociaciones)

Muestra todos los objetos de comunicación que tienen al menos una dirección de grupo vinculada:

| Columna | Descripción |
|---|---|
| Number | Índice del objeto de comunicación |
| Flags | R Lectura (Read) · W Escritura (Write) · C Comunicación (Communication) · T Transmisión (Transmit) · U Actualización (Update) · I Lectura al inicio (Read-on-Init) |
| Size | Tamaño de datos del objeto (1 bit, 1 byte, 2 bytes, etc.) |
| Group addresses | Direcciones de grupo vinculadas a este objeto |

Toca cualquier dirección de grupo para enviarle un comando **Read** o **Write**. Dado que el DPT (tipo de punto de datos) no se puede conocer únicamente a partir de la memoria, se utiliza un campo de entrada de valores en hexadecimal o decimal binario sin procesar, en lugar de una interfaz adaptada a DPT.

Utiliza **Export CSV** o **Export TXT** para exportar la lista de asociaciones de esta sesión.

### Device Info

Muestra la tarjeta de información completa del dispositivo si se ejecutó previamente la acción **Read Full Info**. Incluye un botón **Copy All** para copiar todos los campos al portapapeles.

### Addresses

Una tabla con todas las direcciones de grupo encontradas en la tabla de direcciones de la memoria del dispositivo (índice, formato de 3 niveles, formato de 2 niveles, hexadecimal). Utiliza **Copy All** o **Export CSV** para extraer la lista completa.

---

## Gestión de sesiones

Las sesiones son **persistentes**: se mantienen guardadas tras reiniciar la aplicación y permanecen disponibles hasta que decidas borrarlas.

- **Clear** (situado sobre la lista de tarjetas) — Elimina todas las sesiones almacenadas.
- **Export** (situado sobre la lista de tarjetas) — Exporta todas las sesiones juntas en un único archivo PDF para tus informes de edificios inteligentes.
- **Share** (en la barra superior de la página de detalles de una sesión) — Exporta y comparte únicamente esa sesión específica en formato PDF.

---

## Notas importantes

- Una lectura fallida (borde rojo) suele significar que el dispositivo KNX no responde, se encuentra en estado de error o la dirección física es incorrecta. Utiliza la opción **Check** desde la pestaña Devices para verificar primero si el dispositivo está presente y activo en el bus.
- Si el dispositivo requiere claves de herramienta KNX Data Secure (*tool keys*) para operaciones de gestión de dispositivos, carga el archivo `.knxkeys` en la pestaña **Discovery → Security** antes de proceder con la lectura.
