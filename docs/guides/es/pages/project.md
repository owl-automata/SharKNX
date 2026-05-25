# Página Project

La página Project es la segunda página de la barra de navegación inferior. Es donde cargas un archivo de proyecto ETS y exploras su contenido a través de cuatro vistas estructuradas: Group Addresses, Devices, Topology y Buildings.

---

## Cargar un Proyecto

Pulsa el **folder FAB** para abrir el selector de archivos y seleccionar un archivo `.knxproj`. Si ya has cargado proyectos anteriormente, primero aparecerá una hoja de historial: selecciona una entrada reciente o pulsa **Browse** para elegir un nuevo archivo. Los proyectos protegidos por contraseña son compatibles; la aplicación solicitará la contraseña durante la importación.

Cargar un nuevo proyecto reemplaza el proyecto actualmente cargado. Los datos del proyecto previamente cargado se eliminan de la memoria.

> Para obtener información sobre lo que implica y lo que no implica cargar un proyecto, consulta [ETS Projects in SharKNX](../concepts/ets-project-in-sharknx.md).

---

## Barra de Búsqueda y Filtros

Una vez cargado un proyecto, aparece una barra de búsqueda y filtros debajo de la barra de pestañas. Escribe cualquier texto para buscar entre todos los nombres del proyecto: direcciones de grupo, dispositivos, edificios, líneas y funciones. Los resultados se actualizan mientras escribes dentro de la pestaña activa.

Junto a la barra de búsqueda se encuentra un botón **Expand All / Collapse All** que expande o colapsa todas las secciones de árbol de la pestaña actual de una sola vez.

---

## Banner de KNX Data Secure

Si el proyecto cargado contiene direcciones de grupo KNX Data Secure, aparece un banner debajo de la barra de pestañas solicitando configurar los Data Secure senders. Al pulsar el banner se navega a la página de configuración de Data Secure Senders, donde defines qué dirección física debe utilizar SharKNX como remitente para cada dirección de grupo segura. Esto es necesario para enviar comandos Data Secure; la monitorización funciona sin este paso. Consulta [KNX Data Secure](../concepts/knx-data-secure.md) para más detalles.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-data-secure-banner.png" width="320" alt="Project page with the data secure banner below the tab bar after loading a project with secure group addresses" />
</div>

---

## Pestaña Group Addresses

Esta pestaña muestra la jerarquía de direcciones de grupo tal y como está configurada en ETS: grupos principales en el nivel superior, expandiéndose a grupos intermedios y posteriormente a direcciones de grupo individuales.

Pulsa cualquier grupo principal o intermedio para expandirlo o colapsarlo. Pulsa cualquier **group address** para abrir su hoja de acciones rápidas, que muestra:
- Nombre de la dirección de grupo
- Tipo y subtipo de punto de datos
- Botón **Read** — envía una solicitud de lectura al bus y muestra la respuesta inline en la hoja en menos de 1 segundo si se recibe una respuesta
- Botón **Write** — abre el compositor de comandos con la dirección de grupo y el DPT ya rellenados; introduce un valor y envíalo

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-group-addresses.png" width="320" alt="Group Addresses tab showing the main group tree expanded to individual group addresses" />
</div>

> Debe seleccionarse un gateway para enviar comandos read o write. Si no hay ninguno seleccionado, la aplicación solicitará elegir uno.

---

## Pestaña Devices

Esta pestaña lista todos los dispositivos del proyecto ordenados por dirección física. Los dispositivos que tienen direcciones de grupo conectadas pueden expandirse para mostrar dichas direcciones; pulsa cualquiera de ellas para abrir la misma hoja de acciones rápidas que en la pestaña Group Addresses.

**Pulsa** un dispositivo sin direcciones de grupo o realiza una **long-press** sobre un dispositivo con direcciones de grupo para abrir la **device detail sheet**. Esta hoja contiene:

### Tarjeta Device Info
Una tarjeta compacta que muestra si la dirección física y el programa de aplicación del dispositivo están cargados en el proyecto ETS.

### Acciones Rápidas de Diagnóstico

| Action | What it does |
|---|---|
| **Check** | Comprueba si el dispositivo está presente y responde en el bus |
| **Read Info** | Lee información detallada del dispositivo directamente desde el propio dispositivo (ver más abajo) |
| **Toggle Programming Mode** | Activa o desactiva remotamente el modo programación del dispositivo |
| **Program Address** | Escanea un dispositivo en modo programación y le escribe una nueva dirección física |

**Read Info** recupera lo siguiente del dispositivo:
- Descriptor del dispositivo (por ejemplo, System B)
- Estado del modo programación
- Fabricante y número de pedido
- Versión de firmware
- Estado de carga y estado de ejecución
- Versión de la aplicación
- Estado de la tabla de direcciones y tabla de asociaciones
- Longitud máxima APDU
- Tipo de hardware
- Flags de error y estado del dispositivo

### Botón Communication Objects

Abre la página dedicada **Communication Objects page** para este dispositivo (ver más abajo).

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-device-detail.png" width="320" alt="Device detail bottom sheet showing the info card, four quick action buttons, and the Communication Objects button" />
</div>

---

## Página Communication Objects

Accesible desde el botón Communication Objects en la device detail sheet. Esta página muestra todos los objetos de comunicación del dispositivo que están conectados a al menos una dirección de grupo.

En la parte superior, la página muestra las fechas **last modified** y **last downloaded from ETS** del dispositivo.

Cada entrada de objeto de comunicación muestra:
- Número de objeto
- Flags: Read, Write, Communication, Transmit, Update, Read-on-Init
- Nombre de función (si está disponible en la aplicación del dispositivo)
- Tamaño del objeto (por ejemplo, 1 bit, 1 byte, 2 bytes)
- Direcciones de grupo conectadas — cada una es pulsable para abrir la hoja de acciones rápidas de comandos read/write

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-comm-objects.png" width="320" alt="Communication Objects page showing a list of comm objects with flags, size, and linked group addresses" />
</div>

> La configuración **Load communication objects** en Project Settings controla si estos datos se procesan durante la carga. Está habilitada por defecto. Deshabilitarla reduce el uso de memoria en proyectos grandes, pero elimina el acceso a esta página.

---

## Pestaña Topology

Esta pestaña muestra la topología física del proyecto: áreas en el nivel superior, expandiéndose a líneas o segmentos y posteriormente a dispositivos. Pulsa cualquier dispositivo para abrir la misma device detail sheet descrita anteriormente.

---

## Pestaña Buildings

Esta pestaña muestra la estructura del edificio tal y como está configurada en ETS: edificios y plantas expandiéndose a habitaciones y funciones, con direcciones de grupo y dispositivos debajo. Pulsa cualquier dirección de grupo o dispositivo para abrir sus respectivas hojas de acciones rápidas.

---

## Menú Tune

El icono tune en la barra superior abre una hoja inferior con una acción:

**Unload project** — elimina el proyecto actualmente cargado de la memoria. Las cuatro pestañas vuelven a su estado vacío. Los telegramas capturados en la página Monitor permanecen, pero pierden sus nombres y valores decodificados.
