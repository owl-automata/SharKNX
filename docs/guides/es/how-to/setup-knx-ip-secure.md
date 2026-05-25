# Cómo configurar KNX IP Secure

KNX IP Secure encripta la conexión del túnel entre SharKNX y tu Gateway mediante el algoritmo AES-128 CCM a través de TCP. Antes de que SharKNX pueda conectarse a un Gateway seguro, necesita las credenciales correspondientes. Esta guía explica cómo cargarlas en la aplicación.

Para conocer más a fondo qué protege KNX IP Secure y cómo funciona, consulta la página de concepto [KNX IP Secure](../concepts/knx-ip-secure.md).

---

## Qué necesitas

Uno de los siguientes orígenes de credenciales (todos ellos generados por el software ETS):

| Formato | Cómo obtenerlo |
|---|---|
| Archivo de almacén de claves `.knxkeys` | Exportar desde ETS: Project → Security → Export keystore |
| Archivo de proyecto ETS `.knxproj` | El mismo archivo de proyecto utilizado para cargar las direcciones de grupo; ya contiene las credenciales de los dispositivos |
| Clave de red troncal o Backbone key (cadena hexadecimal) | Se encuentra en ETS, dentro de la configuración de IP Secure de la propia interfaz |

---

## Paso 1 — Abrir la pestaña Security

1. Ve a la página **Discovery**.
2. Toca la pestaña **Security**.

---

## Paso 2 — Cargar las credenciales

Hay tres métodos disponibles. Utiliza el que mejor se adapte a los archivos de los que dispongas:

### Método A — Cargar un archivo de almacén de claves `.knxkeys`

1. Toca en **Load .knxkeys file**.
2. Selecciona el archivo `.knxkeys` desde el almacenamiento de tu dispositivo.
   - Si el archivo está protegido por contraseña, introduce la contraseña del *keystore* cuando la aplicación te lo solicite.
3. Aparecerá una tarjeta de resumen que confirma cuántas credenciales de interfaz se han cargado correctamente.

### Método B — Cargar credenciales desde un archivo de proyecto ETS

Si ya tienes un archivo `.knxproj` cargado o disponible en tu teléfono:

1. Toca en **Load from ETS project**.
2. Selecciona el archivo `.knxproj` (o confirma el proyecto que ya se encuentra cargado).
   - Si el proyecto está protegido por contraseña, introduce la contraseña del proyecto cuando se te solicite.
3. Las credenciales se extraerán del archivo del proyecto y se cargarán de forma automática.

### Método C — Introducir una clave de red troncal (Backbone Key) manualmente

1. Toca en **Enter backbone key**.
2. Pega o escribe la clave hexadecimal de red troncal de 32 caracteres.
3. Confirma. La clave se guardará y se utilizará para cualquier Gateway que la requiera en la instalación.

---

## Paso 3 — Verificar la tarjeta del Gateway

1. Ve a la pestaña **Discover** y realiza un escaneo de Gateways, o abre la pestaña **Config** si tu Gateway ya está guardado en la lista.
2. Localiza tu Gateway seguro. Su tarjeta debería mostrar un **icono de candado**, lo que indica que es compatible con KNX IP Secure.
3. Si las credenciales se cargaron correctamente, el icono del candado aparecerá relleno/activo. Si el icono se muestra vacío o la tarjeta del Gateway presenta una advertencia de credenciales, repite el Paso 2 utilizando el archivo correcto.

---

## Paso 4 — Conectar

1. Toca en **Select** en la tarjeta del Gateway para establecerlo como el Gateway activo.
2. Inicia el monitor de bus (o conéctate desde la página de una Shark Hunt). SharKNX utilizará automáticamente el túnel TCP seguro.
3. Si la conexión se realiza con éxito, el indicador de conexión cambiará a color verde y los telegramas comenzarán a fluir con normalidad para el control KNX.

Si la conexión falla con un error de seguridad, las causas más comunes suelen ser:
- Archivo de almacén de claves (*keystore*) incorrecto (credenciales pertenecientes a un Gateway diferente).
- Contraseña del almacén de claves o del proyecto incorrecta.
- La clave de herramienta (*tool key*) del Gateway se ha renovado en ETS después de exportar el almacén de claves. En este caso, vuelve a exportar el *keystore* desde ETS y cárgalo de nuevo en SharKNX.

---

## Notas importantes

- Las credenciales cargadas a través de archivos `.knxkeys` o `.knxproj` se almacenan de forma local en el dispositivo y se mantienen guardadas tras reiniciar la aplicación. No es necesario volver a cargarlas en cada sesión de diagnóstico de edificios inteligentes.
- Si un archivo `.knxkeys` contiene las claves de herramienta (*tool keys*) de dispositivos individuales (utilizadas para operaciones de gestión de dispositivos), estas también se cargarán en este paso y estarán disponibles en las páginas de Management y Project.
- Puedes ver el historial de los archivos de credenciales cargados anteriormente dentro de la propia pestaña Security.
- Para utilizar un almacén de claves diferente, simplemente carga el nuevo archivo: este reemplazará por completo las credenciales anteriores de la aplicación.
