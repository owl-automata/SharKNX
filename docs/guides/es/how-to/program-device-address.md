# Cómo programar la dirección física de un dispositivo

SharKNX permite programar (escribir) una dirección física (individual) KNX en un dispositivo directamente desde tu teléfono móvil o PC, sin necesidad de recurrir a ETS ni de tener acceso físico a un ordenador portátil en la instalación. Existen dos métodos disponibles: mediante el botón de programación físico o mediante el número de serie del dispositivo (sin necesidad de pulsar ningún botón).

---

## Requisitos previos

- Estar conectado a un Gateway KNX (consulta [Conectarse a un Gateway](connect-to-gateway.md)).
- La nueva dirección física que deseas asignar, ya sea obtenida de tu proyecto o introducida manualmente.

---

## Método A — Mediante el botón de programación

Utiliza este método cuando tengas acceso físico al dispositivo (o cuando un compañero en la obra pueda pulsar el botón por ti).

1. Ve a la pestaña **Management → Line Scan**.
2. Ejecuta un escaneo de línea en el área o línea correspondiente (consulta [Escanear una línea de bus](scan-bus-line.md)), luego toca la tarjeta del dispositivo que deseas reprogramar para abrir su panel de detalles.
   - Alternativamente, puedes ir a la pestaña **Management → Devices**, introducir la dirección física actual del dispositivo y utilizar las acciones desde allí.
3. En el panel de detalles del dispositivo, toca en **Program Address**.
4. Introduce la nueva dirección física en el campo de entrada, o toca el **icono de búsqueda** para seleccionar una de tu proyecto ETS cargado.
5. Toca en **Program via programming button**.
6. La aplicación esperará hasta **20 segundos** a que un dispositivo entre en modo programación. Pulsa el botón de programación en el dispositivo físico durante este intervalo de tiempo.
7. Cuando la app detecte un dispositivo en modo programación, escribirá la nueva dirección y confirmará que el proceso se ha completado con éxito.

> La aplicación comprueba automáticamente si la nueva dirección ya está siendo utilizada por otro dispositivo en la instalación real. Si se detecta un conflicto, se te mostrará una advertencia antes de confirmar la escritura.

---

## Método B — Mediante el número de serie

Utiliza este método si ya dispones del número de serie del dispositivo obtenido en una operación previa de **Read Info**. No requiere pulsar ningún botón físico, lo que lo hace ideal para dispositivos instalados en ubicaciones de difícil acceso en tus edificios inteligentes.

1. Asegúrate primero de que el número de serie del dispositivo sea conocido: realiza un **Read Info** desde la tarjeta del dispositivo en Line Scan o desde la pestaña Devices si aún no lo has hecho.
2. En el panel de detalles del dispositivo o en la pestaña Devices, toca en **Program Address**.
3. Introduce la nueva dirección física o selecciónala desde el proyecto.
4. Toca en **Program via serial number**.
5. La aplicación se comunicará con el dispositivo directamente utilizando su número de serie y escribirá la nueva dirección sin necesidad de activar el botón de programación.

---

## Consejo — Alternar el modo programación de forma remota

Si no puedes alcanzar físicamente el botón de programación, utiliza la opción **Toggle Programming Mode** desde la tarjeta del dispositivo o desde la pestaña Devices para activarlo de forma remota en primer lugar. Acto seguido, ejecuta inmediatamente **Program via programming button**: la app lo detectará dentro del margen de 20 segundos. No olvides desactivarlo de nuevo al terminar.

---

## Notas importantes

- Tras realizar la programación, verifica el resultado tocando en **Check** en la tarjeta del dispositivo para confirmar que la nueva dirección física está activa y responde en el bus KNX.
- Este flujo de trabajo es ideal para la fase de puesta en marcha inicial: escanear la línea → identificar todos los dispositivos → programar las direcciones físicas → conectarse y descargar los programas definitivos desde el software ETS.
