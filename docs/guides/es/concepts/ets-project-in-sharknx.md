# Proyectos ETS en SharKNX

SharKNX puede cargar un archivo de proyecto estándar de ETS (`.knxproj`) para enriquecer cada parte de la aplicación con los nombres, los tipos de punto de datos y la estructura que ya has definido en ETS. Esta página explica lo que esto significa en la práctica: qué hace SharKNX con el archivo, qué no hace y qué hay que tener en cuenta.

---

## El archivo de proyecto nunca se modifica

Cargar un archivo `.knxproj` en SharKNX es una operación de solo lectura. SharKNX lee el archivo una vez, extrae los datos que necesita y los almacena internamente. **El archivo original en tu dispositivo nunca se sobrescribe ni se modifica.** No tienes que preocuparte de que SharKNX corrompa tu proyecto, cree conflictos de versiones o cause problemas cuando vuelvas a abrir el mismo proyecto en ETS más adelante.

---

## Lo que desbloquea cargar un proyecto

Sin un proyecto, SharKNX sigue funcionando: puedes conectarte a una pasarela, monitorizar el bus y enviar comandos utilizando direcciones de grupo en bruto. Todo es funcional pero no tiene nombre. Cargar un proyecto cambia la experiencia significativamente:

**Página de Project — cuatro vistas estructuradas:**
Las pestañas de Group Addresses, Devices, Topology y Buildings se rellenan con los datos de tu proyecto, reflejando la estructura que tienes en ETS. Puedes explorar toda la jerarquía, buscar en todos los nombres y tocar cualquier dirección de grupo para enviar un comando de lectura o escritura directamente.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-group-addresses.png" width="320" alt="Project page showing the group address tree with main groups, middle groups, and group addresses from a loaded ETS project" />
</div>

**Página de Monitor — telegramas decodificados y con nombre:**
Los telegramas entrantes se vinculan automáticamente al proyecto cargado. Cada fila de telegrama muestra el nombre de la dirección de grupo y un valor decodificado legible por humanos basado en su tipo de punto de datos, en lugar de solo una carga útil (payload) en hexadecimal. El compositor de comandos utiliza el proyecto para rellenar previamente el nombre de la dirección de grupo y el DPT al tocar una dirección de grupo.

**KNX Data Secure — extracción automática de claves:**
Si tu proyecto contiene direcciones de grupo KNX Data Secure, sus claves de grupo se extraen automáticamente. SharKNX las utiliza para desencriptar los telegramas data secure entrantes en el monitor y para encriptar los comandos data secure salientes. No es necesario realizar un paso independiente de importación de credenciales para la seguridad a nivel de grupo. Consulta [KNX Data Secure](knx-data-secure.md) para más detalles.

---

## Objetos de comunicación

Cuando el ajuste **Load communication objects** (Cargar objetos de comunicación) está activado (por defecto), SharKNX también analiza y almacena los objetos de comunicación de cada dispositivo que tiene direcciones de grupo conectadas a él. Esto añade una capa adicional de detalle:

- En la pestaña Devices (Dispositivos), puedes abrir una página dedicada a los objetos de comunicación de cada dispositivo, mostrando todos los objetos de comunicación conectados con sus flags (banderas), tamaños, funciones y direcciones de grupo vinculadas.
- Esto es especialmente útil para el diagnóstico de dispositivos: puedes ver de un vistazo qué objetos de comunicación están mapeados a qué direcciones de grupo y enviar comandos de prueba directamente desde esa vista.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-comm-objects.png" width="320" alt="Communication objects page for a device showing object number, flags, function, size, and linked group addresses" />
</div>

Desactivar este ajuste reduce el uso de memoria, lo cual puede ser relevante en dispositivos con RAM limitada o para proyectos muy grandes. El resto de los datos del proyecto (direcciones de grupo, topología, edificios) se sigue cargando con normalidad.

---

## Lo que SharKNX no hace

SharKNX es una herramienta de campo, no una herramienta de puesta en marcha (commissioning). Hay cosas que deliberadamente no hace con el proyecto de ETS:

- **Sin cambios de parámetros.** SharKNX no puede leer ni modificar los parámetros de los dispositivos almacenados en el proyecto. Solo ETS puede escribir parámetros en los dispositivos.
- **Sin descarga de programas de aplicación.** SharKNX no puede programar ni flashear dispositivos con su software de aplicación. Esto sigue siendo exclusivo de ETS.
- **Sin conexión a un servidor ETS o licencia.** SharKNX lee el archivo exportado `.knxproj` directamente. No se conecta a ETS, no requiere que ETS se esté ejecutando y no consume una licencia de ETS.

**La programación de direcciones individuales** (Programming individual addresses) es la única operación de escritura compatible con SharKNX que se relaciona con los datos del proyecto, pero se escribe directamente en el dispositivo físico en el bus a través de la comunicación de gestión KNX, no en el archivo `.knxproj`. El archivo de proyecto en sí permanece inalterado.

---

## Mantener actualizados los datos del proyecto

SharKNX lee el archivo de proyecto en el momento en que lo cargas. Si posteriormente realizas cambios en ETS y exportas un nuevo `.knxproj`, SharKNX no recogerá esos cambios automáticamente: deberás volver a cargar el archivo actualizado.

La función **Apply project data** (Aplicar datos del proyecto) en el menú de ajustes de la página de Monitor ayuda con esto: después de cargar un proyecto actualizado, puedes aplicar los nuevos nombres y tipos de punto de datos a los telegramas ya capturados en la lista del monitor, sin tener que volver a grabar una sesión.

---

## Formatos compatibles

| Formato | Compatible |
|---|---|
| `.knxproj` (ETS5) | ✅ |
| `.knxproj` (ETS6) | ✅ |
| Proyectos protegidos por contraseña | ✅ (pide la contraseña al importar) |
| `.knxpkg` u otros formatos ETS | — |

Solo se puede cargar un proyecto a la vez. Cargar un proyecto nuevo reemplaza al actual. Los proyectos cargados anteriormente se guardan en un historial para poder recargarlos rápidamente sin tener que volver a navegar por el sistema de archivos.
