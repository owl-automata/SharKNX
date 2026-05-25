# Cómo conectarse a un Gateway KNX

SharKNX se conecta a tu instalación de domótica KNX a través de un Gateway KNXnet/IP en la red local. Esta guía explica cómo descubrir un Gateway automáticamente, guardarlo para un uso rápido, añadir uno manualmente y establecer el control KNX.

---

## Opción A — Escanear y conectar (Recomendado para el primer uso)

1. Ve a la página **Discovery** y abre la pestaña **Discover**.
2. Toca el **botón flotante (FAB) de escaneo** (icono de radar). La aplicación envía solicitudes de descubrimiento KNXnet/IP en la red local y muestra una lista con todos los Gateways que responden.
3. Localiza tu Gateway en los resultados. Cada tarjeta muestra el nombre del Gateway, la dirección IP, el puerto y si es compatible con **KNX IP Secure**.
4. Toca **Select** en la tarjeta del Gateway para establecerlo como el Gateway activo para la sesión actual.
   - Para guardarlo para futuras sesiones, toca **Save** en la tarjeta. Los Gateways guardados aparecen en la pestaña **Config** y se pueden seleccionar sin necesidad de volver a escanear.
5. Ve a la página **Monitor** (o a cualquier página que requiera conexión) y toca el **botón flotante (FAB) connect/start**. SharKNX se conectará al Gateway seleccionado automáticamente, facilitando la gestión de tus edificios inteligentes.

> **Último Gateway seleccionado:** El Gateway que utilizaste más recientemente se recuerda y se muestra en la parte superior de la ventana emergente de conexión en las páginas Monitor y Shark Hunt. Esto significa que normalmente no necesitarás visitar la página Discovery de nuevo tras la primera configuración.

---

## Opción B — Añadir un Gateway manualmente

Utiliza esta opción cuando el Gateway esté en una subred diferente o no sea detectable mediante multicast (por ejemplo, para el acceso remoto a tu instalación domótica a través de VPN).

1. Ve a la página **Discovery** y abre la pestaña **Config**.
2. Toca el **botón flotante (FAB) +** para abrir el formulario manual de Gateway.
3. Completa los campos requeridos:

   | Campo | Descripción |
   |---|---|
   | **Name** | Una etiqueta para identificar este Gateway en la lista |
   | **IP address** | La dirección IPv4 del Gateway |
   | **Port** | El valor por defecto es `3671` |
   | **Use KNX IP Secure** | Actívalo si el Gateway requiere un túnel seguro |
   | **NAT mode** | Actívalo si te conectas a través de un router NAT o firewall |

4. Toca **Save**. El Gateway aparecerá en la lista de la pestaña Config y estará disponible inmediatamente para su selección.
5. Toca la entrada del Gateway para seleccionarlo, luego inicia el monitor o conéctate desde una página *Hunt*.

> La pestaña Config admite hasta **50** Gateways guardados.

---

## Opción C — Conectar vía Multicast (KNX IP Routing)

Si tu instalación utiliza un **IP Router** KNX en modo *routing*, SharKNX puede recibir y enviar telegramas en el grupo multicast en lugar de crear un túnel a través de un Gateway específico.

1. Ve a la página **Discovery** → pestaña **Discover**.
2. Si no se encuentra ningún IP Router con capacidad de *routing* durante el escaneo, es posible que la sección multicast no aparezca por defecto. Activa **Always show multicast options** en **Settings → Discover** para que sea permanentemente visible.
3. Toca **Select** en la opción multicast. No es necesario configurar ninguna dirección IP ni puerto: la aplicación utiliza la dirección multicast y el puerto configurados en Settings → Discover (por defecto: `224.0.23.12`, puerto `3671`).

---

## Conexión con KNX IP Secure

Si el Gateway requiere KNX IP Secure, carga tus credenciales en la pestaña **Security** de la página Discovery antes de conectarte. Consulta [Configurar KNX IP Secure](setup-knx-ip-secure.md).

---

## Solución de problemas

| Síntoma | Causa probable |
|---|---|
| No se encuentran Gateways tras el escaneo | El dispositivo y el Gateway están en subredes diferentes, o el tráfico multicast está bloqueado. Intenta usar **Force unicast subnet scan** en Settings → Discover, o añade el Gateway manualmente |
| Tiempo de espera de conexión agotado (Timeout) | La IP o el puerto del Gateway son incorrectos, o el Gateway está ocupado con otro cliente (la mayoría de los Gateways solo admiten un túnel simultáneo) |
| La conexión segura falla | Las credenciales no se han cargado, o el *keystore* es incorrecto. Revisa la pestaña Security |
| Gateway encontrado pero no se puede seleccionar | El Gateway podría requerir KNX IP Secure y las credenciales aún no se han cargado |
