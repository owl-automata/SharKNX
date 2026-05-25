# Cómo configurar KNX Data Secure

KNX Data Secure encripta los telegramas KNX individuales en la capa de aplicación. Para recibir y enviar telegramas seguros correctamente, SharKNX necesita las claves de grupo de tu proyecto ETS y, para el envío, una dirección física de emisor configurada. Esta guía detalla ambos pasos.

Para conocer más a fondo el funcionamiento de KNX Data Secure, consulta la página de concepto [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Requisitos previos

- Un archivo de proyecto ETS `.knxproj` que incluya direcciones de grupo con KNX Data Secure activado.
- Una dirección física (individual) KNX que SharKNX pueda utilizar como su identidad de emisor. Esta dirección debe existir en el proyecto ETS y tener derechos de acceso asignados a las direcciones de grupo a las que pretendas realizar los envíos.

> **Restricción de KNX IP Secure:** El envío mediante KNX Data Secure requiere que el monitor de bus se esté ejecutando a través de un túnel KNX IP Secure. Si tu Gateway no es compatible con KNX IP Secure, existen dos soluciones alternativas desde ETS — consulta la página de concepto [KNX Data Secure](../concepts/knx-data-secure.md#sending-constraints) para más detalles.

---

## Parte 1 — Cargar las claves de grupo

Las claves de grupo se encuentran incrustadas dentro del propio archivo `.knxproj`. Cargar el proyecto en la aplicación es suficiente: SharKNX extraerá las claves de forma totalmente automática.

1. Ve a la página **Project**.
2. Toca el **botón flotante (FAB) de la carpeta** para abrir el selector de archivos, o selecciona un proyecto cargado recientemente de la lista del historial.
3. Selecciona tu archivo `.knxproj`.
   - Si el proyecto está protegido por contraseña, introdúcela cuando se te solicite.
4. Una vez cargado, comprueba el **Data Secure banner** en la parte superior de la página Project. Si aparece, significa que el proyecto contiene direcciones de grupo Data Secure y las claves se han cargado correctamente.

---

## Parte 2 — Configurar la dirección física del emisor (Sender Address)

SharKNX necesita saber qué dirección física KNX debe utilizar al enviar telegramas con KNX Data Secure. Sin esto, los envíos seguros fallarán.

1. Desde la página **Project**, toca en el **Data Secure banner**. Esto abrirá el panel de configuración del emisor (*sender configuration sheet*).
   - Alternativamente, navega a **Project → pestaña Devices**, busca el dispositivo cuya dirección deseas utilizar como emisor y accede a la configuración del emisor desde allí.
2. En el panel de configuración del emisor, elige uno de los dos métodos disponibles:

### Opción A — Configurar una dirección física específica

1. Toca en **Add sender address**.
2. Introduce la dirección física (por ejemplo, `1.1.250`), o toca el icono de búsqueda para seleccionar un dispositivo directamente desde el proyecto cargado.
3. Confirma los cambios. La dirección se guardará como un emisor de confianza.

### Opción B — Utilizar la dirección de emisor global (automática)

Si prefieres no especificar direcciones físicas individuales de forma manual:

1. Toca en **Set global sender address**.
2. Introduce la dirección física que se utilizará para todos los envíos seguros.

SharKNX empleará esta dirección para cualquier dirección de grupo Data Secure que no tenga una dirección física de emisor específica configurada.

> Si ninguna de las opciones cuenta con una dirección que figure en la lista de emisores de confianza del proyecto ETS para una dirección de grupo determinada, el dispositivo receptor rechazará el telegrama. Asegúrate de que la dirección que configures haya sido añadida a la lista de emisores del objeto de grupo dentro de ETS.

---

## Parte 3 — Verificación

1. Inicia el monitor de bus (conéctate a tu Gateway y toca el botón FAB de inicio en la página Monitor).
2. Provoca el envío de un telegrama Data Secure en el bus KNX (por ejemplo, pulsando un interruptor físico en la instalación).
3. El telegrama debería aparecer en la lista del monitor con su valor completamente decodificado (y no solo en formato hexadecimal raw). Esto confirma que la clave de grupo se ha aplicado correctamente.
4. Para verificar el envío: desde el monitor, mantén presionado un telegrama correspondiente a una dirección de grupo Data Secure para abrir el compositor de comandos ya precargado con su dirección y DPT. Envía un comando de escritura (Write). El dispositivo de la instalación domótica debería responder de la forma esperada.

---

## Notas importantes

- Las claves de grupo se vuelven a leer cada vez que cargas un proyecto. Si las claves se han renovado en ETS (por ejemplo, tras una nueva puesta en marcha), vuelve a cargar el archivo de proyecto para obtener las claves actualizadas.
- Las direcciones de emisor se mantienen guardadas tras reiniciar la aplicación. Solo necesitas configurarlas una vez por proyecto.
- El indicador de Data Secure en la página Monitor y en las páginas de Shark Hunts muestra el estado actual del emisor de un vistazo: el color ámbar significa que los emisores aún no se han configurado, mientras que el verde indica que el sistema está listo.
