# Shark Hunts

Un Shark Hunt es un conjunto de acciones reutilizable y autónomo para probar y diagnosticar una instalación KNX. En lugar de navegar a una dirección de grupo, seleccionar un punto de datos y componer un comando cada vez que necesites ejecutar una prueba, construyes un hunt una vez y lo ejecutas con un solo toque: desde cualquier lugar y en cualquier visita a la misma instalación.

---

## La idea principal

Cada Shark Hunt se almacena como un archivo JSON que describe una colección de **acciones de envío** (comandos al bus) y **acciones de monitorización** (sesiones de monitor filtradas). Un hunt puede contener uno de los dos tipos, o ambos. Cuando abres un hunt, todas sus acciones se presentan en una sola página de tarjetas interactivas, listas para ejecutarse.

Esto hace que los Shark Hunts sean útiles en varios escenarios:

- **Pruebas repetitivas.** La puesta en marcha a menudo requiere enviar los mismos comandos docenas de veces en múltiples visitas a la obra. Un hunt captura esos comandos para que nunca tengas que reconstruirlos.
- **Delegar diagnósticos.** Un hunt puede incluir todos los detalles de conexión para una instalación específica. Puedes exportarlo y compartirlo con un colega o cliente, quien luego lo ejecuta en su propio dispositivo sin necesidad de saber cómo configurar una pasarela o encontrar una dirección de grupo.
- **Secuencias de prueba estructuradas.** Una acción múltiple/secuencia puede enviar una serie de comandos con retrasos configurables entre ellos, cubriendo una prueba completa de escena de iluminación o un ciclo de persianas con un solo toque.
- **Filtrado avanzado de bus.** Las acciones de monitorización pueden aplicar lógicas de filtro complejas (combinando rangos de direcciones de grupo, filtros de dispositivos, filtros de tipos de telegrama y ventanas de tiempo) que la barra de filtros estándar del monitor no soporta.

---

## Acciones de envío

Hay tres tipos de acciones de envío disponibles:

**Send Fixed** (Envío fijo) ejecuta un único comando de escritura o lectura a una dirección de grupo específica con un valor fijo cada vez. Útil para activadores rápidos de dispositivos: encender una luz, guardar una escena, comprobar el valor de un sensor.

**Send Multiple / Sequence** (Envío múltiple / Secuencia) ejecuta una serie de comandos fijos en orden. Cada comando en la secuencia puede tener un retraso configurable antes de que se dispare el siguiente (hasta 10 segundos por paso). Úsalo para probar el guardado de escenas, secuencias de movimiento de persianas o cualquier lógica de automatización de múltiples pasos.

**Send Variable** (Envío variable) envía un valor que tú eliges en el momento de la ejecución a una o más direcciones de grupo que comparten el mismo tipo de punto de datos. Cuando tocas la tarjeta de la acción, se abre una hoja de entrada de valores con los controles DPT correspondientes (deslizadores, selectores de color, campos numéricos, etc.). Útil cuando quieres flexibilidad para probar diferentes valores sin editar el hunt.

---

## Acciones de monitorización

Hay tres tipos de acciones de monitorización disponibles:

**Custom Monitor** (Monitor personalizado) aplica un filtro de múltiples condiciones al monitor de bus. Las condiciones pueden filtrar por dirección de grupo (incluyendo comodines como `1/*/0`), por dirección individual del remitente (incluyendo comodines como `1.*.*`), por tipo de telegrama (lectura, escritura, respuesta), por nombre o texto de descripción, y por ventana de tiempo. Las condiciones se conectan con lógica AND/OR, lo que permite crear filtros que no se pueden expresar a través de la barra de búsqueda estándar del monitor. Las entradas de direcciones y dispositivos también se pueden configurar para excluir en lugar de incluir, para que puedas monitorizar todo excepto un rango específico.

**Monitor Space** (Monitorizar espacio) utiliza la estructura de edificios de tu proyecto de ETS para establecer el objetivo del filtro. Seleccionas una habitación o espacio de la jerarquía del edificio y el monitor muestra solo las direcciones de grupo o dispositivos que pertenecen a ese espacio. No se necesita introducir manualmente ninguna dirección.

**Monitor Device** (Monitorizar dispositivo) apunta a uno o más dispositivos específicos de tu proyecto de ETS y monitoriza todas las direcciones de grupo conectadas a ellos. Efectivo para aislar la comunicación de un solo actuador o sensor durante las pruebas.

Cuando abres una acción de monitorización en un hunt, los filtros se aplican inmediatamente. Una etiqueta (badge) en la vista del monitor muestra los detalles del filtro activo, y una hoja de cambio rápido te permite alternar entre todas las acciones de monitorización en el hunt sin salir de la página del monitor.

---

## Compartir y portabilidad

Los Shark Hunts están diseñados para ser compartidos. Cada hunt puede incluir opcionalmente una **pasarela preconfigurada**: la dirección IP, el puerto y los ajustes de conexión para la instalación para la que fue creado. Cuando alguien abre un hunt compartido, esa pasarela aparece como una opción de conexión para que puedan conectarse y ejecutar el hunt sin necesidad de descubrir o configurar nada por sí mismos.

Puedes exportar un solo hunt o todos tus hunts a la vez como un archivo JSON, y luego compartirlo a través de cualquier método de transferencia de archivos (apps de mensajería, correo electrónico, unidades en la nube). Importar un archivo JSON añade los hunts que contiene a tu lista sin sobrescribir los existentes.

Las tarjetas de los hunts están codificadas por colores para que puedas ver de un vistazo qué hace un hunt:

| Color del borde | Contenido |
|---|---|
| Verde | Solo acciones de envío |
| Azul | Solo acciones de monitorización |
| Rojo | Tanto acciones de envío como de monitorización |

---

## Persistencia

Los hunts se guardan en el dispositivo y persisten tras reiniciar la app. Las marcas de tiempo de creación y de última modificación para cada hunt se almacenan y son visibles en la hoja de información del hunt.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-main-page.png" width="320" alt="Shark Hunts main page showing hunt cards with colour-coded borders" /></td>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="An open Shark Hunt page showing send action cards and monitor action cards" /></td>
    </tr>
  </table>
</div>

---

## Lecturas complementarias

- [Create a Shark Hunt](../how-to/create-shark-hunt.md) — guía paso a paso para construir tu primer hunt
