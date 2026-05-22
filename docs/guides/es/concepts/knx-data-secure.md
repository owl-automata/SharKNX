# KNX Data Secure

KNX Data Secure es la extensión de seguridad de la capa de aplicación para el estándar KNX. Encripta y autentica telegramas KNX individuales en el medio de bus (TP o RF), protegiéndolos de la interceptación y manipulación independientemente de cómo se transporten a la red IP.

> Esta página explica qué es KNX Data Secure y cómo lo gestiona SharKNX. Para ver el procedimiento de configuración paso a paso, consulta [Set Up KNX Data Secure](../how-to/setup-knx-data-secure.md).

---

## Qué protege KNX Data Secure

Los telegramas KNX estándar transmitidos a través de par trenzado son legibles por cualquier dispositivo en el mismo segmento de bus. KNX Data Secure soluciona esto encriptando los datos de aplicación de telegramas de grupo seleccionados mediante **AES-128 CCM**, el mismo cifrado utilizado por KNX IP Secure. Cada telegrama encriptado también incluye un **Código de Autenticación de Mensajes (MAC)** y un **número de secuencia** incremental, que en conjunto evitan:

- Escuchas pasivas (Eavesdropping): la carga útil (payload) del telegrama no se puede leer sin la clave de grupo.
- Manipulación (Tampering): cualquier modificación en la carga útil invalida el MAC.
- Ataques de repetición (Replay attacks): un telegrama capturado no se puede volver a reproducir porque su número de secuencia estaría fuera de orden.

KNX Data Secure opera en la capa de aplicación de KNX, dentro del propio telegrama. Es independiente de la ruta de transporte; un telegrama data secure está igual de protegido tanto si viaja por TP, RF o a través de un túnel KNXnet/IP.

---

## Claves de grupo y la lista de remitentes

Cada dirección de grupo KNX Data Secure tiene su propia **clave de grupo**. La clave se utiliza tanto para encriptar la carga útil como para calcular el MAC. Se almacena en el llavero (keyring) del proyecto de ETS y se distribuye a todos los dispositivos conectados a esa dirección de grupo durante la puesta en marcha.

Además de la encriptación, los dispositivos KNX Data Secure mantienen una **lista de remitentes de confianza** por dirección de grupo: un conjunto de direcciones individuales cuyos telegramas serán aceptados por el dispositivo. Los telegramas que lleguen desde una dirección individual que no esté en esta lista se descartan silenciosamente, incluso si la encriptación es correcta. Esto significa que:

- Para **recibir** telegramas data secure correctamente, necesitas la clave de grupo.
- Para **enviar** comandos data secure sobre los que un dispositivo deba actuar, tu dirección individual debe estar en la lista de remitentes de confianza del dispositivo para esa dirección de grupo.

---

## Recibir telegramas Data Secure en SharKNX

SharKNX extrae todas las claves de grupo data secure automáticamente cuando cargas un archivo `.knxproj`. No se requiere una configuración de credenciales independiente para la monitorización. Una vez cargado un proyecto:

- Los telegramas data secure entrantes en el Monitor se desencriptan de forma transparente y se muestran con su valor decodificado, nombre y tipo de punto de datos, exactamente igual que los telegramas no seguros.
- Si no hay ningún proyecto cargado, los telegramas data secure aparecen en hexadecimal puro sin valor decodificado (la carga útil está encriptada y es ilegible sin la clave).

La **etiqueta de Data Secure** en la fila de etiquetas de la página de Monitor refleja el estado actual: atenuada si no hay direcciones de grupo data secure presentes en el proyecto cargado, ámbar si las direcciones data secure están cargadas pero los remitentes no se han configurado, y verde cuando los remitentes están configurados y el envío está listo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-project-banner.png" width="320" alt="Project page with the data secure banner prompting sender configuration after loading a project with data secure group addresses" />
</div>

---

## Enviar telegramas Data Secure — la dirección de remitente

Cuando SharKNX envía un comando data secure, debe presentar una dirección individual que el dispositivo de destino reconozca como un remitente de confianza. Si la dirección no está en la lista de remitentes del dispositivo, el comando se ignora.

SharKNX gestiona esto a través de la configuración de **Data Secure Senders**, accesible desde el banner que aparece en la página de Project cuando se carga un proyecto con direcciones de grupo data secure.

En la página de remitentes puedes:

- Establecer una **dirección de remitente global**: se utiliza para cualquier dirección de grupo data secure que no tenga una dirección específica configurada.
- Establecer **excepciones por dirección**: mapea direcciones de grupo individuales a direcciones individuales de remitente específicas.
- **Autogenerar a partir de los datos del proyecto**: SharKNX lee el proyecto de ETS y crea automáticamente los mapeos entre dirección de grupo ↔ dirección individual según qué dispositivos estén conectados a cada dirección de grupo segura. Esta es la forma más rápida de configurar los remitentes cuando tienes un proyecto completo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-senders.png" width="320" alt="Data Secure Senders configuration page showing global sender and per-address mapping list" />
</div>

---

## La restricción de la dirección de remitente con KNX IP Secure

Cuando SharKNX se conecta a través de un **túnel KNX IP Secure**, la dirección individual utilizada en todos los telegramas salientes la fija la pasarela con la dirección de la interfaz de la conexión de túnel. SharKNX no puede invalidar esta dirección; es una propiedad del protocolo KNX IP Secure.

Esto crea una restricción práctica: para que un dispositivo data secure acepte comandos de SharKNX a través de un túnel KNX IP Secure, la dirección de la interfaz de túnel ya debe estar en la lista de remitentes de confianza del dispositivo en ETS.

Dos enfoques funcionan bien en la práctica:

1. **Usar una interfaz virtual (dummy) dedicada en ETS.** Crea un dispositivo de interfaz segura virtual en tu proyecto de ETS y conecta todas las direcciones de grupo data secure a él. Asigna su dirección individual como el remitente en SharKNX. Esto mantiene el acceso de SharKNX limpiamente separado de otros clientes.

2. **Conectar las direcciones de grupo data secure a la interfaz de túnel de la pasarela.** En ETS, asocia las direcciones de grupo data secure con la interfaz de conexión de túnel de tu pasarela KNX IP Secure. Cualquier cliente que se conecte a través de esa interfaz (incluyendo SharKNX) será reconocido entonces como un remitente de confianza por los dispositivos de campo.

> Si te estás conectando sin KNX IP Secure (túnel estándar no encriptado), SharKNX puede usar cualquier dirección individual que configures como remitente, y esta restricción no se aplica.

---

## Claves de herramienta (Tool Keys) para la gestión de dispositivos

KNX Data Secure también se aplica a las operaciones de gestión de dispositivos: lectura de información del dispositivo, conmutación del modo de programación, reinicio de un dispositivo, programación de una dirección individual o lectura de tablas de comunicación. Los dispositivos que requieren autenticación a nivel de herramienta rechazarán los comandos de gestión de fuentes desconocidas.

Cuando cargas un archivo `.knxkeys` en la **pestaña Security** de la página de Discovery, SharKNX extrae automáticamente cualquier **clave de herramienta (tool key)** presente en el archivo y la almacena. Estas claves permiten la comunicación encriptada de gestión de dispositivos con los correspondientes dispositivos Data Secure; no se necesita ninguna configuración adicional una vez que las claves están cargadas.

Las claves de herramienta son independientes de las claves de grupo integradas en el archivo `.knxproj`. Si tu instalación utiliza la gestión de dispositivos Data Secure, necesitas tener el archivo `.knxkeys` (o el archivo `.knxproj`, que también contiene claves de herramienta) cargado en la pestaña Security, además del proyecto cargado en la página de Project.

---

## Lecturas complementarias

Para obtener una explicación técnica detallada del protocolo KNX Data Secure, la nota de aplicación de ABB "i-bus KNX Data Secure" es un recurso exhaustivo que cubre en profundidad los mecanismos criptográficos, la gestión de números de secuencia y la configuración en ETS.

---

## KNX Data Secure vs. KNX IP Secure

| | KNX Data Secure | KNX IP Secure |
|---|---|---|
| **Alcance** | Telegrama KNX (capa de aplicación) | Capa de transporte IP |
| **Qué encripta** | Telegramas de grupo individuales en el medio KNX | El túnel UDP/TCP o canal multicast |
| **Tipo de credencial** | Clave de grupo por dirección de grupo; claves de herramienta por dispositivo | Credenciales de interfaz; clave de línea troncal (backbone) |
| **Dónde se configura en SharKNX** | Página de Project (claves de `.knxproj`); pestaña Security (claves de herramienta) | Página de Discovery → pestaña Security |
| **Requerido para** | Enviar/recibir telegramas de grupo seguros | Conectarse a una pasarela KNX IP Secure |

Ambos mecanismos son independientes y pueden utilizarse por separado o en conjunto. Consulta [KNX IP Secure](knx-ip-secure.md) para ver su contraparte en la capa de transporte.
