# Referencia de Settings

La **Settings page** es accesible desde cualquier pantalla tocando el **gear icon** (⚙️) en la esquina superior derecha de la barra de la aplicación, lo que resulta fundamental para gestionar su **instalación domótica**.

La página agrupa todas las opciones configurables en secciones. Un **search icon** (🔍) en la barra superior le permite saltar directamente a una sección por su nombre.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-overview.png" width="320" alt="Página de Settings — lista completa de secciones" />
</div>

---

## Discover Settings

Controla cómo la aplicación busca y se conecta a las pasarelas (gateways) KNX IP en la red de su sistema de **control KNX**.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-a.png" width="320" alt="Discover Settings (1 de 2)" /></td>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-b.png" width="320" alt="Discover Settings (2 de 2)" /></td>
    </tr>
  </table>
</div>

### Multicast

| Setting | Default | Descripción |
|---|---|---|
| Multicast address | `224.0.23.12` | La dirección de grupo multicast IP utilizada para el descubrimiento y enrutamiento (routing) KNX IP. Cámbiela solo si su red utiliza un grupo multicast no estándar en su **domótica KNX**. |
| Multicast port | `3671` | El puerto UDP utilizado para la comunicación de descubrimiento multicast y enrutamiento (routing). |

### Discovery behaviour

| Setting | Default | Descripción |
|---|---|---|
| Always show multicast options | Off | Cuando está habilitado, las opciones de conexión multicast siempre están visibles en la pestaña **Discover tab**. Cuando está deshabilitado, solo aparecen si se encuentra un KNX IP Router con capacidades de routing durante un escaneo de la red. |
| Force unicast subnet scan | Off | Cuando está habilitado, después de enviar solicitudes de descubrimiento multicast, la aplicación también envía solicitudes de búsqueda unicast individuales a cada dirección IP en la subred actual. Útil en redes Wi-Fi donde los routers pueden descartar paquetes multicast. Si no se encuentra ninguna pasarela a través de multicast, siempre se ejecuta automáticamente un escaneo unicast como respaldo (fallback), independientemente de esta configuración. |

### Timeouts

| Setting | Default | Min | Max | Descripción |
|---|---|---|---|---|
| Discovery timeout | 3 s | 1 s | 10 s | El tiempo que la aplicación espera las respuestas de la pasarela después de enviar solicitudes de descubrimiento. Aumente este valor en redes lentas o congestionadas típicas de grandes **edificios inteligentes**. |
| Connection timeout | 3 s | 1 s | 10 s | El tiempo que la aplicación espera al intentar establecer una conexión de túnel (tunnelling) con una pasarela antes de tratarla como inalcanzable. |

---

## Project Settings

Controla cómo se analizan y muestran los archivos del proyecto **ETS**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-project.png" width="320" alt="Project Settings" />
</div>

| Setting | Default | Descripción |
|---|---|---|
| Load communication objects | On | Cuando está habilitado, la aplicación analiza y almacena los objetos de comunicación para cada dispositivo en el proyecto que tiene al menos una dirección de grupo conectada a él. Deshabilitar esto reduce el uso de memoria en proyectos grandes, pero elimina la vista **Communication Objects view** de la página **Project page**. |
| Items per page | 50 | Min: 20 · Max: 200 — El número de elementos que se muestran a la vez al expandir una lista en la vista de árbol del proyecto (por ejemplo, direcciones de grupo dentro de un grupo intermedio). Una vez que se alcanza el límite, aparece un botón **Load more**. Valores más bajos mejoran la velocidad de renderizado en proyectos grandes. |

---

## Monitor Settings

Controla el comportamiento del monitor del bus, esencial para un correcto **diagnóstico KNX**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-monitor.png" width="320" alt="Monitor Settings" />
</div>

| Setting | Default | Descripción |
|---|---|---|
| Keep screen on | On | Evita que la pantalla del dispositivo se apague mientras una sesión de monitorización está activa. Recomendado porque la mayoría de los sistemas operativos móviles cerrarán la conexión IP cuando la pantalla se apague. Desactívelo para conservar batería, pero tenga en cuenta que la monitorización se detendrá si la pantalla se apaga. Nota: el monitor siempre se detiene cuando la aplicación pasa a segundo plano, independientemente de este ajuste. |
| Telegram buffer size | 2000 | Min: 50 · Max: 5000 — El número máximo de **telegramas** que se mantienen en el **búfer** de la lista del monitor en cualquier momento. Cuando se alcanza el límite, los **telegramas** más antiguos se sobrescriben con los entrantes. Aumente este valor si necesita un historial más largo; disminúyalo para reducir el uso de memoria en dispositivos de gama baja. |

---

## Scan Settings

Controla el escaneo en modo de programación en la página **Management** page → pestaña **Prog. Mode** tab.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-scan.png" width="320" alt="Scan Settings" />
</div>

| Setting | Default | Min | Max | Descripción |
|---|---|---|---|---|
| Scan duration | 10 s | 4 s | 20 s | Duración total de un escaneo en modo de programación. La aplicación escucha a los dispositivos que están en modo de programación durante este período de tiempo. |
| Scan interval | 2 s | 1 s | 4 s | Con qué frecuencia la aplicación envía señales de escaneo durante una sesión. Un intervalo más corto aumenta la posibilidad de detectar un dispositivo que ingresa brevemente al modo de programación, a costa de un mayor tráfico de red. |

---

## Subscription

Muestra el estado de su suscripción actual y proporciona opciones de gestión del plan.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-subscription.png" width="320" alt="Subscription" />
</div>

| Item | Descripción |
|---|---|
| Current plan | Muestra su plan activo: **Free** (prueba), **Monthly**, **Yearly** o **Lifetime**. |
| Restore purchases | Vuelve a aplicar una suscripción comprada previamente al dispositivo actual. Use esto después de reinstalar la aplicación o cambiar de dispositivo. |
| Cancel subscription | Abre la página de gestión de suscripciones en la App Store (iOS/macOS) o Google Play (Android), donde puede cancelar una suscripción recurrente activa. No aplicable a planes **Lifetime**. |
| Privacy Policy | Enlace a la [Privacy Policy](../../privacy/privacy-en.md) de la aplicación. |
| Terms of Service | Enlace a los [Terms of Service](../../terms/terms-en.md) de la aplicación. |

---

## Language

Abre una lista de los idiomas de interfaz compatibles con la aplicación. La selección de un idioma tiene efecto inmediato sin necesidad de reiniciar la aplicación.

Idiomas disponibles:

- 🇬🇧 English
- 🇩🇪 German
- 🇫🇷 French
- 🇪🇸 Spanish
- 🇮🇹 Italian

---

## Theme

Establece la apariencia visual de la aplicación.

| Option | Descripción |
|---|---|
| Light | Utiliza siempre la combinación de colores claros. |
| Dark | Utiliza siempre la combinación de colores oscuros. |
| Match system | Sigue la configuración del modo claro/oscuro de todo el sistema del dispositivo. |

---

## Send Feedback

| Option | Descripción |
|---|---|
| Leave a review | Abre la ficha de la tienda de la aplicación para que pueda dejar una calificación o reseña. |
| Report a bug | Abre un correo electrónico con dirección previa a `info@owl-automata.com` para informar de un problema. |
| Write to us | Abre un correo electrónico en blanco a `info@owl-automata.com` para consultas generales. |

> Para obtener informes de errores estructurados, consulte también la guía [How to Report an Issue](../../../support/how-to-report-an-issue.md).

---

## About

Muestra el número de versión actual de la aplicación y la información de derechos de autor.
