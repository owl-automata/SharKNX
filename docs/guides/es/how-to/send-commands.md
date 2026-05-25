# Cómo enviar comandos KNX

SharKNX puede enviar tanto comandos de lectura como de escritura a cualquier dirección de grupo KNX mientras el monitor de bus está activo. Esta guía explica el funcionamiento del compositor de comandos (Command Composer), todos los puntos de acceso desde los que se puede abrir y cómo utilizar las etiquetas de envío rápido (chips) para comandos repetitivos.

---

## Requisitos previos

- Tener un Gateway seleccionado y el monitor en ejecución (consulta [Conectarse a un Gateway](connect-to-gateway.md)).
- Opcionalmente, un proyecto ETS cargado para que los nombres de las direcciones de grupo y los tipos de punto de datos (DPT) se completen automáticamente.

---

## El compositor de comandos (Command Composer)

El compositor de comandos es el núcleo de la interfaz de envío de la aplicación. Cuenta con cuatro campos principales:

| Campo | Descripción |
|---|---|
| **Group address** | La dirección de grupo KNX de destino. Escríbela manualmente (por ejemplo, `1/2/3`) o toca el icono de búsqueda para explorar tu proyecto ETS cargado. |
| **Command type** | **Write** para enviar un valor (escritura), **Read** para solicitar el valor actual (lectura). |
| **DPT** | El tipo y subtipo de punto de datos (por ejemplo, DPT 1.001 — Conmutación). Se rellena automáticamente si seleccionas la dirección desde los datos del proyecto. |
| **Value** | Para comandos de tipo *Write*: el valor que deseas enviar, presentado en una interfaz adaptada al DPT (interruptor, barra de desplazamiento, selector de color, campo numérico, etc.). |

Toca en **Send** para transmitir el comando. Este aparecerá inmediatamente en la lista de telegramas del monitor.

---

## Puntos de acceso (Entry Points)

### Desde la página Monitor (Método principal)

1. Inicia el monitor: el botón flotante (FAB) verde de inicio se convertirá en un **botón FAB de envío rojo**.
2. Toca el **botón FAB de envío**.
3. Se abrirá un panel inferior (*bottom sheet*). Toca en **New command** para abrir el compositor de comandos.
4. Rellena los campos y toca en **Send**.

### Quick-Send Chips (Etiquetas de envío rápido)

Después de enviar un comando, aparecerá una **etiqueta (chip)** en el panel inferior que muestra la dirección de grupo y el valor enviado. Estas etiquetas se mantienen guardadas durante toda la sesión.

- **Toca una etiqueta** para reenviar instantáneamente el mismo comando sin necesidad de volver a abrir el compositor.
- **Mantén presionada una etiqueta** para reabrir el compositor de comandos con la dirección de grupo y el DPT ya cumplimentados (muy útil para reenviar el comando con un valor diferente).

### Desde un telegrama en la lista del Monitor

1. Toca cualquier fila de telegrama para abrir su panel de detalles.
2. Toca en **Write**: se abrirá el compositor de comandos con la dirección de grupo y el DPT ya precargados desde el telegrama.
3. Introduce el valor y toca en **Send**.

El panel de detalles también incluye un botón **Read** que envía una solicitud de lectura inmediatamente sin necesidad de abrir el compositor.

### Desde la página Project — Pestaña Group Addresses

1. Ve a la página **Project → pestaña Group Addresses**.
2. Navega por el árbol de direcciones y toca cualquier dirección de grupo individual.
3. En el panel inferior, toca en **Write** para abrir el compositor de comandos precargado con la dirección y su DPT, o toca en **Read** para lanzar un comando de lectura inmediatamente.

### Desde la página Project — Pestaña Devices

1. Ve a la página **Project → pestaña Devices**.
2. Despliega un dispositivo y toca cualquier dirección de grupo vinculada que aparezca bajo él.
3. Aparecerá el mismo panel inferior: toca en **Write** o **Read**.

### Desde la página de Objetos de Comunicación (Communication Objects)

1. Ve a la página **Project → pestaña Devices**.
2. Toca un dispositivo (o mantén presionado un dispositivo que tenga direcciones de grupo asignadas) para abrir su panel de detalles.
3. Toca en **Communication Objects** para abrir la página de objetos de comunicación de ese dispositivo específico.
4. Toca cualquier dirección de grupo que se muestre debajo de un objeto de comunicación: aparecerá el mismo panel inferior de lectura/escritura preconfigurado con la dirección y el DPT.

### Desde la pestaña Inspect — Associations

Cuando has reconstruido las tablas de comunicación de un dispositivo en la pestaña **Management → Inspect**, la pestaña Associations muestra todas las direcciones de grupo encontradas en la memoria del dispositivo.

1. Toca cualquier dirección de grupo en la pestaña Associations.
2. Dado que el DPT no se puede extraer únicamente de la memoria del dispositivo, se mostrará un **campo de entrada de valor sin procesar** (en lugar de una interfaz adaptada a DPT). Introduce un valor decimal o hexadecimal y envíalo.
3. También dispones de un botón **Read** para enviar una solicitud de lectura a esa dirección.

---

## Enviar un comando de lectura (Read Command)

Una solicitud de lectura pide al dispositivo KNX que contiene el estado actual de esa dirección de grupo que responda enviando su valor al bus. El telegrama de respuesta aparecerá en la lista del monitor. Si la aplicación ya estaba monitorizando el bus cuando tocaste **Read** desde la página Project, escuchará la respuesta para esa dirección durante aproximadamente un segundo y mostrará el resultado directamente en el panel inferior.

---

## Notas importantes

- El envío de comandos solo es posible mientras el monitor de bus se encuentra en ejecución. Las tarjetas de acción en las Shark Hunts son la única excepción: estas se conectan y realizan el envío de forma independiente en cada *hunt*.
- Si estás trabajando con una dirección de grupo con seguridad **KNX Data Secure**, la dirección física del emisor debe estar configurada previamente para que el dispositivo acepte las escrituras seguras. Consulta [Configurar KNX Data Secure](setup-knx-data-secure.md).
- Los comandos que envías aparecen en la lista del monitor de la misma manera que cualquier otro telegrama, lo que te permite comprobar inmediatamente si el bus KNX ha confirmado su recepción (*ACK*).
