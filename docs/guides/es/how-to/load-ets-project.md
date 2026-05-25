# Cómo cargar un proyecto ETS

Cargar un archivo `.knxproj` le da acceso a SharKNX a los nombres de las direcciones de grupo, los tipos de punto de datos (DPT), los metadatos de los dispositivos y las claves para KNX Data Secure. Sin un proyecto cargado, el monitor solo mostrará valores en hexadecimal sin procesar y sin nombres.

---

## Antes de comenzar

El archivo `.knxproj` ya debe estar guardado en tu dispositivo móvil. Si aún no lo está, transfiérelo primero usando uno de estos métodos:
- Compartiéndolo desde el software ETS directamente a tu teléfono a través de una app de mensajería, correo electrónico o AirDrop.
- Guardándolo en una unidad en la nube (iCloud, Google Drive, OneDrive) para abrirlo desde allí.
- Transfiriéndolo mediante un cable USB.

SharKNX es compatible con archivos `.knxproj` creados en **ETS5 y ETS6**, incluyendo proyectos protegidos por contraseña.

---

## Pasos a seguir

1. Ve a la página **Project** (la segunda pestaña en la barra de navegación inferior).
2. Toca el **botón flotante (FAB) de la carpeta**.
   - Si ya has cargado proyectos anteriormente, se abrirá un **historial desplegable**. Toca cualquier entrada para volver a cargarlo al instante, sin necesidad de buscar el archivo de nuevo.
   - Para cargar un archivo nuevo por primera vez, toca en **Browse** (o el botón del selector de archivos) para abrir el explorador de archivos del sistema.
3. Selecciona tu archivo `.knxproj`.
4. Si el proyecto está **protegido por contraseña**, introdúcela cuando la aplicación te lo solicite y confirma.
5. El proyecto se cargará. En ese momento se activarán la barra de búsqueda, el botón de expandir/contraer y las cuatro pestañas principales (Group Addresses, Devices, Topology, Buildings).

---

## Qué cambia después de cargar el proyecto

- La **página Monitor** y el **monitor de las Shark Hunts** ahora mostrarán los nombres de las direcciones de grupo y los valores decodificados de los telegramas entrantes.
- La barra de búsqueda de la **página Project** te permitirá filtrar todos los elementos de tu edificio inteligente, dispositivos y direcciones de grupo por su nombre.
- Si el proyecto contiene direcciones de grupo configuradas con **KNX Data Secure**, aparecerá un banner informativo debajo de la barra de pestañas. Toca en él para configurar las direcciones físicas de envío antes de emitir comandos seguros. Consulta [Configurar KNX Data Secure](setup-knx-data-secure.md).

---

## Cargar el proyecto desde otras pantallas

No es obligatorio navegar hasta la página Project para cargar un proyecto. El **indicador de proyecto ETS (ETS Project badge)** en la página Monitor y en las páginas de Shark Hunts incluye un botón **Load project** cuando no hay ningún proyecto activo; al tocarlo, se abrirá el mismo historial y el selector de archivos.

---

## Actualizar o reemplazar un proyecto

SharKNX mantiene activo un solo proyecto a la vez. Para cambiar a una exportación más reciente de tu instalación domótica o a un proyecto diferente:

1. Toca de nuevo el **botón flotante (FAB) de la carpeta** en la página Project (o en el indicador de proyecto ETS en cualquier otra parte de la app).
2. Selecciona el archivo `.knxproj` actualizado.
3. El nuevo proyecto reemplazará al anterior de forma inmediata.

> Si el monitor de bus está activo mientras cargas un nuevo proyecto, los cambios se aplicarán a los nuevos telegramas entrantes. Los telegramas que ya están en la lista mantendrán los metadatos del proyecto anterior hasta que se limpie la lista.

Para descargar un proyecto por completo sin poner otro en su lugar, toca el **icono de ajustes (sintonización/rueda)** en la página Project y selecciona **Unload project**.

---

## Notas importantes

- Cargar un proyecto incorrecto (uno que no coincida con tu instalación KNX física) provocará que se muestren nombres erróneos y valores decodificados incorrectos en el monitor. Verifica siempre que estás utilizando el proyecto adecuado para la obra en la que estás trabajando.
- El archivo del proyecto se lee una sola vez al cargarse. SharKNX no se mantiene conectado a ETS de forma remota y no detectará los cambios realizados en el software ETS después de haber cargado el archivo. Vuelve a cargar el archivo `.knxproj` tras realizar modificaciones en ETS.
- SharKNX nunca modifica ni altera el archivo `.knxproj` original.
