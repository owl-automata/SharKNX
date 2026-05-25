# Cómo escanear una línea de bus KNX

El escaneo de una línea de bus (Line Scan) sondea cada dirección física en una línea KNX específica y muestra una lista con todos los dispositivos que responden. Esto te permite verificar qué componentes están instalados realmente —de forma totalmente independiente de cualquier proyecto ETS— y es el método más rápido para obtener una visión general de una instalación domótica desconocida.

---

## Requisitos previos

- Estar conectado a un Gateway KNX (consulta [Conectarse a un Gateway](connect-to-gateway.md)).
- Conocer el número de área y de línea KNX que deseas escanear (por ejemplo: área 1, línea 1 → `1.1`).

---

## Pasos a seguir

1. Ve a la pestaña **Management → Line Scan**.
2. En la tarjeta **Scan Settings**, configura los parámetros del escaneo:

   | Ajuste | Descripción |
   |---|---|
   | **Area / Line** | El área y línea que vas a escanear (por ejemplo, `1.1`). Toca en **Choose from project** para seleccionar una línea directamente de tu proyecto ETS cargado (esto también configurará el tipo de medio automáticamente). |
   | **Medium type** | TP (par trenzado), IP o IoT. Debe coincidir con el medio físico real de la línea. |
   | **Range** | Dirección de inicio y fin del dispositivo dentro de la línea (0–255). Puedes acotar este rango para acelerar el escaneo o comprobar un segmento específico. |

3. Toca el **botón flotante (FAB) de escaneo** para comenzar. El escaneo se puede detener en cualquier momento.
4. Los dispositivos descubiertos irán apareciendo en forma de tarjetas. El color del borde superior indica el tipo de dispositivo:

   | Color | Tipo |
   |---|---|
   | Azul | Acoplador KNX (Line/Area Coupler) |
   | Rojo | Dispositivo de aplicación estándar |
   | Verde | Dispositivo KNX Secure |

---

## Leer la información de todos los dispositivos descubiertos

Una vez que el escaneo haya finalizado, toca en **Read Device Info** (situado sobre la lista de tarjetas). La aplicación leerá de forma secuencial el fabricante, el número de serie y otros detalles de cada uno de los dispositivos encontrados en el bus KNX.

Esto es especialmente útil para:
- Crear rápidamente un inventario de una instalación de edificios inteligentes que tú no hayas puesto en marcha.
- Contrastar los datos con un proyecto ETS para verificar si coincide exactamente con la instalación física.
- Localizar dispositivos con direcciones físicas inesperadas o tipos incorrectos.

---

## Trabajar con las tarjetas de dispositivo individuales

Toca cualquier tarjeta para abrir su panel de detalles. Desde allí podrás realizar las siguientes acciones de diagnóstico KNX:

- **Check** — Verificar si el dispositivo sigue respondiendo y está activo en el bus.
- **Read Info** — Leer los detalles completos del dispositivo (fabricante, versión de firmware, estado de ejecución, etc.).
- **Toggle Programming Mode** — Activar o desactivar el modo programación de forma remota.
- **Restart** — Enviar un comando de reinicio al dispositivo.
- **Program Address** — Asignar una nueva dirección física (consulta [Programar la dirección física de un dispositivo](program-device-address.md)).
- **Rebuild Communication** — Abre la pestaña Inspect con la dirección de este dispositivo ya cumplimentada para leer sus tablas de comunicación directamente.

---

## Exportar los resultados del escaneo

Toca el **icono de ajustes (sintonización/rueda)** en la barra superior para exportar el resultado del escaneo más reciente:
- **Export as text** — Genera un informe en formato TXT con la marca de tiempo del escaneo, el Gateway utilizado, el área/línea, el medio físico y la lista de dispositivos.
- **Export as PDF** — Exporta el mismo contenido en un informe PDF profesional.
