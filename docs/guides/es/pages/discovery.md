# Página Discovery

La página Discovery es la primera página de la barra de navegación inferior y se abre por defecto cuando se inicia la aplicación. Es el lugar donde puedes encontrar, configurar y gestionar gateways KNX IP para conectarte a ellos. Dispone de tres pestañas: **Discover**, **Config** y **Security**.

---

## Pestaña Discover

Pulsa el **scan FAB** para comenzar la búsqueda de dispositivos KNX IP en la red local. La aplicación envía solicitudes de búsqueda KNX IP y muestra cualquier dispositivo que responda como tarjetas.

### Tarjetas de Gateway

Cada tarjeta de gateway descubierta muestra:
- Nombre del gateway (tal y como lo anuncia el dispositivo)
- Dirección IP y puerto de túnel

Cada tarjeta incluye dos botones:

**Select** — marca este gateway como el destino de conexión activo. El gateway se mueve a la sección **Last Selected Gateway** en la parte superior de la página y se recuerda incluso después de reiniciar la aplicación. Seleccionar un gateway no establece una conexión inmediata; la aplicación se conecta automáticamente cuando realizas una acción (iniciar el monitor, enviar un comando, etc.).

**Save** — guarda el gateway en la pestaña **Config** para reutilizarlo sin necesidad de volver a descubrirlo. Muy útil cuando visitas regularmente la misma instalación domótica o realizas tareas de diagnóstico KNX.

Al pulsar una tarjeta (no un botón) se abre la **gateway detail sheet**:
- Dirección física KNX
- Número de serie
- Dirección MAC
- Tipo de medio
- Capacidades de gestión del dispositivo (si son compatibles)
- Botón **Connect** — conecta inmediatamente; útil para probar la accesibilidad, aunque no es necesario para el funcionamiento normal
- Botón **Load Credentials** *(solo gateways KNX IP Secure)* — carga credenciales `.knxkeys` o `.knxproj` para este gateway. Consulta [KNX IP Secure](../concepts/knx-ip-secure.md).

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-scan.png" width="320" alt="Discover tab showing discovered gateway cards with Select and Save buttons" /></td>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-gateway-detail.png" width="320" alt="Gateway detail bottom sheet showing address, serial number, MAC, and Connect button" /></td>
    </tr>
  </table>
</div>

### Last Selected Gateway

Si anteriormente se ha seleccionado un gateway, aparecerá en una sección fijada en la parte superior de la pestaña Discover. Se vuelve a seleccionar automáticamente al reiniciar la aplicación para que puedas continuar trabajando en tu sistema de control KNX sin volver a escanear.

### Sección Multicast

Si se detecta un KNX IP Router con capacidades de routing, aparecerá una sección **Multicast** debajo de la lista de tarjetas. Al expandirla se muestran dos opciones:
- **Multicast** — multicast estándar KNX IP en `224.0.23.12:3671`
- **Secure Multicast** — multicast cifrado que requiere una clave backbone (consulta [KNX IP Secure](../concepts/knx-ip-secure.md))

Selecciona cualquiera de las opciones para utilizarla como tipo de conexión en lugar de un túnel unicast.

---

## Pestaña Config

La pestaña Config almacena gateways que has guardado manualmente o mediante el botón **Save** en la pestaña Discover. Los gateways disponibles aquí pueden utilizarse en cualquier momento sin necesidad de escanear nuevamente la red de la instalación domótica KNX.

### Añadir un Gateway Manualmente

Pulsa el **"+" FAB** para abrir la página de configuración manual del gateway. Completa los siguientes campos:

| Field | Description |
|---|---|
| Friendly name | Etiqueta mostrada en la tarjeta para identificar este gateway |
| IP address / hostname | Dirección IP del gateway o nombre DNS (por ejemplo, un dominio DynDNS) |
| KNX individual address | Dirección física KNX del gateway; el valor por defecto es `15.15.255`. Debe coincidir con el dispositivo para conexiones KNX IP Secure. |
| Port | Puerto de túnel; valor por defecto `3671` |
| Use NAT | Habilitar para escenarios VPN donde el cliente y el gateway están en diferentes subredes |
| KNX IP Secure | Marca esta conexión como una conexión KNX IP Secure |

Pulsa **Save** para crear la entrada. El gateway aparecerá como una tarjeta en la pestaña Config.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-config-manual.png" width="320" alt="Manual gateway configuration page with fields for name, IP, port, and secure options" />
</div>

### Tarjetas de Gateway en Config

Las tarjetas en la pestaña Config funcionan de forma idéntica a las de la pestaña Discover (Select, Save, detail sheet) con una diferencia adicional: un botón **Edit** que vuelve a abrir la página de configuración para corregir o actualizar cualquier campo sin necesidad de eliminar y recrear la entrada.

La pestaña Config admite un máximo de 50 gateways guardados.

---

## Pestaña Security

La pestaña Security es donde se cargan las credenciales KNX IP Secure y KNX Data Secure que se aplican en toda la aplicación para tareas de control KNX y diagnóstico KNX.

Pulsa el **shield FAB** para abrir la hoja de importación de credenciales. Hay disponibles tres métodos de entrada:

| Method | Use case |
|---|---|
| `.knxkeys` file | Exportado desde ETS. Contiene credenciales de interfaz, clave backbone y claves de herramienta. Requiere la contraseña del almacén de claves definida durante la exportación. |
| `.knxproj` file | Exportación completa de un proyecto ETS. SharKNX extrae automáticamente todas las credenciales seguras. |
| Manual backbone key | Introduce directamente una clave backbone multicast en formato hex. Solo para secure multicast. |

Después de la carga, la pestaña muestra un resumen:
- Cuántas interfaces KNX IP se encontraron en el archivo
- Cuántos dispositivos KNX Data Secure (por dirección física) estaban presentes

Un botón **History** en la parte superior permite recargar rápidamente archivos de credenciales utilizados recientemente sin necesidad de navegar nuevamente por el sistema de archivos.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-security-tab.png" width="320" alt="Security tab showing a loaded credential file summary with interface and device counts" />
</div>

> **Claves de herramienta:** Un archivo `.knxkeys` también puede contener claves de herramienta para dispositivos KNX Data Secure. Si están presentes, SharKNX las almacena automáticamente para habilitar operaciones cifradas de gestión de dispositivos (activar modo programación, leer información del dispositivo, etc.). Consulta [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Menú Tune

El icono tune en la barra superior abre una hoja inferior con acceso rápido a la carga de credenciales sin necesidad de navegar hasta la pestaña Security:

- **Load credentials from .knxkeys** — abre el selector de archivos para un archivo `.knxkeys`
- **Load credentials from .knxproj** — abre el selector de archivos para un archivo `.knxproj`
