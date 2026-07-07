# Guía de inicio con SharKNX

SharKNX es un compañero de campo profesional de KNX para dispositivos móviles y de escritorio. Esta guía te acompañará a través del flujo de trabajo principal: conectarse a una pasarela KNX IP, cargar un proyecto de ETS y de iniciar una sesión de monitor de bus en vivo.

## Requisitos previos

- Un dispositivo con Android, iOS, Windows o macOS 13+
- Una pasarela KNX IP accesible en la misma red IP que tu dispositivo
- (Recomendado) Un archivo de proyecto de ETS (`.knxproj`) de tu instalación

> **Suscripción:** SharKNX requiere una suscripción activa. Sin una suscripción o prueba activa, solo podrás cargar un proyecto ETS y no podrás conectarte a pasarelas (gateways) ni a multidifusión (multicast). Los planes mensuales y anuales incluyen una prueba gratuita de 14 días. También está disponible un plan de por vida como pago único. Consulta [Subscription Plans](reference/subscription-plans.md) para más detalles.

---

## Paso 1 — Descubrir tu pasarela

La página de **Discovery** se abre automáticamente cuando se inicia la aplicación. Es la página situada más a la izquierda en la barra de navegación inferior.

1. Toca el **FAB de escaneo** en la parte inferior de la página.  
   La aplicación enviará peticiones de búsqueda KNX IP a través de tu red local. Cualquier pasarela KNX IP que responda aparecerá en forma de tarjeta en la lista.

2. Toca **Select** en la tarjeta de la pasarela que quieras utilizar.  
   La pasarela se moverá a la sección **Last Selected Gateway** en la parte superior de la página y se recordará en los próximos inicios; no será necesario escanear de nuevo en la siguiente sesión.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-discovery.png" width="320" alt="Discovery tab showing a discovered gateway card with Select and Save buttons" />
</div>

> **¿No se encuentran pasarelas?** Verifica que tu dispositivo esté en el mismo segmento de red que la pasarela. En redes Wi-Fi con una VLAN cableada, el router podría descartar los paquetes multicast. Utiliza la pestaña **Config** para añadir la pasarela manualmente mediante su dirección IP y puerto, o activa la opción **Force unicast subnet scan** en los ajustes de Discover.

> **¿KNX IP Secure?** Si tu pasarela requiere credenciales de KNX IP Secure, toca la tarjeta de la pasarela y utiliza el botón **Load Credentials**. Consulta [Set Up KNX IP Secure](how-to/setup-knx-ip-secure.md) para ver el procedimiento completo.

> **Guardar para más tarde:** Toca **Save** en la tarjeta de una pasarela para almacenarla permanentemente en la pestaña **Config**. Las pasarelas guardadas estarán disponibles sin necesidad de volver a escanear, lo cual es muy útil cuando vuelves a visitar la misma instalación.

---

## Paso 2 — Cargar tu proyecto de ETS

Un proyecto de ETS le proporciona a SharKNX los nombres de las direcciones de grupo, los tipos de punto de datos y los metadatos de los dispositivos de tu instalación. Sin él, los telegramas se muestran como valores hexadecimales puros, sin nombres ni valores decodificados.

1. Toca la página de **Project** (segunda pestaña en la barra de navegación inferior).
2. Toca el **FAB de carpeta** para abrir el selector de archivos. Navega hasta tu archivo `.knxproj` y selecciónalo.  
   Si ya has cargado proyectos anteriormente, aparecerá primero un historial; selecciona una entrada reciente o toca **Browse** para elegir un archivo nuevo.
3. Espera a que el proyecto termine de cargarse. Las cuatro pestañas (Group Addresses, Devices, Topology, Buildings) se rellenarán con los datos de tu proyecto.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-load-project.png" width="320" alt="Project page with the group address tree expanded after loading an ETS project" />
</div>

> **Cómo llevar el archivo a tu dispositivo:** Exporta tu proyecto de ETS desde tu PC (`Archivo → Exportar proyecto` o haz clic derecho sobre el proyecto en ETS). Después, transfiere el archivo `.knxproj` a tu móvil usando el método que prefieras: enviándotelo a ti mismo a través de una app de mensajería (por ejemplo, guardándolo en tu propio chat en Viber, WhatsApp o Telegram), adjuntándolo a un correo electrónico, subiéndolo a una nube (Google Drive, iCloud, OneDrive) y abriéndolo en tu teléfono, o copiándolo mediante USB.

> **Proyectos protegidos con contraseña** están soportados. La app te pedirá la contraseña del proyecto durante la importación.

> **Saltarse este paso:** Puedes monitorizar el bus sin un proyecto. Los telegramas mostrarán únicamente las direcciones de origen y destino en bruto con sus cargas útiles en hexadecimal.

---

## Paso 3 — Iniciar el monitor de bus

1. Toca la página de **Monitor** (cuarta pestaña en la barra de navegación inferior).
2. Toca el **FAB verde de inicio**.
   - Si aún no se ha seleccionado ninguna pasarela, aparecerá un selector con la lista de tus pasarelas descubiertas y guardadas; selecciona una para continuar.
   - La app se conectará a la pasarela y comenzará a recibir telegramas.
3. Los telegramas entrantes aparecerán como filas en la lista. Cada fila muestra:
   - Dirección individual del remitente → dirección de grupo de destino
   - Nombre de la dirección de grupo y valor decodificado *(requiere un proyecto de ETS)*
   - Carga útil en hexadecimal puro
   - Marca de tiempo en formato `HH:MM:SS.ms`

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-monitor-active.png" width="320" alt="Monitor page with live telegrams in the list view" />
</div>

> Toca cualquier fila de telegrama para abrir sus detalles, que incluyen el origen, el destino, el valor decodificado y botones para enviar un comando inmediato de **Read** o **Write** a esa dirección.

> **Mantener la pantalla encendida:** El monitor se detiene si la pantalla del móvil se bloquea. El modo de pantalla encendida está activado por defecto en los ajustes de Monitor para evitar esto.

---

## Paso 4 — Enviar un comando

Con el monitor en funcionamiento, puedes enviar comandos de prueba sin necesidad de salir de la vista de monitorización.

1. Toca el **FAB rojo de envío** (este sustituye al FAB de inicio una vez que el monitor está activo).
2. Toca **New Command** en la hoja inferior.
3. En el compositor de comandos:
   - Introduce una dirección de grupo, o toca el **icono de búsqueda** para explorar las direcciones de grupo de tu proyecto cargado.
   - Elige **Write** o **Read**.
   - Selecciona el tipo y subtipo de punto de datos.
   - Para la escritura, introduce el valor que deseas enviar.
4. Toca **Send**. El comando se transmitirá al bus y aparecerá en la lista de telegramas inmediatamente.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-send-command.png" width="320" alt="Command composer page showing group address input, DPT selector, and value field" />
</div>

> **Reenvío rápido:** Tras enviar un comando, aparecerá una etiqueta (chip) con su dirección y valor cerca del FAB de envío. Toca la etiqueta para volver a enviarlo inmediatamente, o manténla pulsada para reabrir el compositor con los campos ya rellenados.

---

## Siguientes pasos

Ahora ya tienes una sesión de monitorización en vivo, un proyecto de ETS cargado, y sabes cómo enviar comandos de prueba. A partir de aquí:

| Objetivo | Guía |
|---|---|
| Explorar direcciones de grupo y enviar comandos desde el árbol del proyecto | [Project Page](pages/project.md) |
| Crear conjuntos de filtros y comandos reutilizables | [Shark Hunts](concepts/shark-hunts.md) |
| Configurar la decodificación de direcciones de grupo con KNX Data Secure | [Set Up KNX Data Secure](how-to/setup-knx-data-secure.md) |
| Escanear una línea de bus y comprobar la presencia de dispositivos | [Scan Bus Line](how-to/scan-bus-line.md) |
| Exportar tu sesión de monitor a CSV o PDF | [Export Formats](reference/export-format.md) |
| Leer la información del firmware de un dispositivo o conmutar el modo de programación | [Inspect Device](how-to/inspect-device.md) |
