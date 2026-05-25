# Formatos de Exportación

SharKNX puede exportar datos en cinco formatos dependiendo de la fuente en su **instalación domótica**:

| Formato | Origen | Extensión |
|--------|--------|-----------|
| [Telegram CSV](#telegram-csv) | Monitor, Shark Hunt Monitor | `.csv` |
| [Line Scan Text](#line-scan-text) | Scan page → resultados de Line Scan | `.txt` |
| [Line Scan PDF](#line-scan-pdf) | Scan page → resultados de Line Scan | `.pdf` |
| [Device Tables PDF](#device-tables-pdf) | Inspect page → tablas de dispositivo | `.pdf` |
| [Shark Hunt JSON](#shark-hunt-json) | Shark Hunts page | `.json` |

En dispositivos móviles, el archivo exportado se ofrece a través de la hoja para compartir del sistema operativo. En ordenadores de escritorio (Windows, macOS), se abre un cuadro de diálogo nativo de guardado de archivo o carpeta, facilitando la gestión del **control KNX**.

---

## Telegram CSV

Exportado desde la Monitor page y desde cualquier página Shark Hunt Monitor usando el botón export/save o el tune menu, ideal para un detallado **diagnóstico KNX**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-telegram-sheet.png" width="320" alt="Hoja inferior de exportación de telegramas" />
</div>

### Nombre de archivo

```
SharKNX_[Context]_YYYY-MM-DD_HHMMSS.csv
```

`[Context]` es `Monitor` o el nombre del Shark Hunt (saneado, máximo 30 caracteres). Ejemplo: `SharKNX_Monitor_2026-05-16_143022.csv`.

### Estructura del archivo

La primera línea es siempre un comentario de identificación:

```
# SharKNX Export v1
```

A esto le sigue una fila de encabezado opcional y luego una fila de datos por cada **telegrama**.

### Columnas seleccionables por el usuario

Estas columnas se alternan individualmente en la hoja inferior de exportación antes de guardar:

| Columna | Encabezado | Descripción |
|--------|--------|-------------|
| ID | `ID` | Posición secuencial del **telegrama** en la lista |
| Time | `Time` | Marca de tiempo en formato `HH:MM:SS.mm` |
| Source | `Source` | Dirección física del dispositivo emisor |
| Destination | `Destination` | Dirección de grupo del **telegrama** |
| Name | `Name` | Nombre de la dirección de grupo desde el proyecto **ETS** (vacío si no hay proyecto cargado) |
| Type | `Type` | Tipo APCI: `Write`, `Read`, `Response`, etc. |
| Value | `Value` | Valor decodificado desde el proyecto **ETS** (vacío si no hay proyecto cargado) |
| Raw | `Raw` | Carga útil RAW como cadena hex; siempre presente en los datos del bus |

### Columnas de metadatos

Cinco columnas estructurales **siempre se añaden** independientemente de la selección del usuario. Se utilizan para la importación de ida y vuelta a SharKNX:

| Columna | Tipo | Descripción |
|--------|------|-------------|
| `_timestampMs` | integer | Marca de tiempo Unix en milisegundos |
| `_isGroupAddress` | boolean | Si el destino es una dirección de grupo |
| `_priority` | string | Campo de prioridad **KNX** |
| `_hopCount` | integer | Conteo de saltos (hop count) de la trama del **telegrama** |
| `_numericValue` | float | Representación numérica del valor decodificado (si está disponible) |

### Opciones

| Option | Default | Descripción |
|--------|---------|-------------|
| Delimiter | Comma | Separador de campos: `,`, `;`, o tabulación |
| Include headers | On | Escribe los nombres de las columnas como primera fila de datos |
| Max telegrams | All | Limita opcionalmente a las primeras N filas |

### Importación

Un archivo CSV de SharKNX se puede volver a importar en el Monitor a través del tune menu → **Import SharKNX CSV**. El archivo debe tener la línea de encabezado `# SharKNX Export v1`. La importación sobrescribe la lista actual de telegramas.

**Archivo de muestra:** [sample-telegrams.csv](../../../../assets/examples/exports/sample-telegrams.csv)

---

## Line Scan Text

Exportado desde la Scan page una vez que se completa un escaneo de línea (Line Scan), a través del utilities menu → **Export as Text**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-scan-utilities.png" width="320" alt="Menú de utilidades de Scan page mostrando opciones de exportación" />
</div>

### Nombre de archivo

```
line_scan_{area.line}_{YYYY-MM-DD}.txt
```

Ejemplo: `line_scan_1.1_2026-05-16.txt`.

### Estructura del archivo

El informe está dividido en tres secciones separadas por líneas discontinuas.

**Bloque de encabezado**

```
Generated     : 2026-05-16 14:30:22
ETS Project   : My Building
Gateway       : Secure Tunnel  192.168.2.7:3671  (1.1.0)
Line          : 1.1
Medium        : TP
Range         : 0 - 255
Devices Found : 12
Duration      : 38s
```

**Lista de dispositivos** — tabla numerada compacta:

```
  [1]   1.1.1    MDT SCN-00.02        (0x0900)
  [2]   1.1.5    Siemens 5WG1...      (0xFFFF)  [DataSecure]
  ...
```

Cada fila muestra: índice, dirección física, cadena del modelo, descriptor hex, y una bandera `[DataSecure]` si el descriptor es `0xFFFF`.

**Resultados detallados** — un bloque por dispositivo, con cuatro subsecciones para el análisis de su **domótica KNX**:

| Subsección | Campos |
|------------|--------|
| Identity | Descriptor, Device Role, Device Name, DataSecure |
| Hardware | Serial No., Manufacturer, Order Info, Firmware version, Hardware Type, Max APDU length |
| Application | Load State, Run State, App Version, Address Table load state, Association Table load state, Group Object Table load state |
| Status | Programming Mode, Error Flags, Device Control |

Los campos que no se leyeron (por ejemplo, si no se activó **Read Info** para un dispositivo) se muestran como `–`.

**Archivo de muestra:** [sample-line-scan.txt](../../../../assets/examples/exports/sample-line-scan.txt)

---

## Line Scan PDF

Exportado desde la Scan page una vez que se completa un escaneo de línea (Line Scan), a través del utilities menu → **Export as PDF**.

### Nombre de archivo

```
line_scan_{area.line}_{YYYY-MM-DD}.pdf
```

Ejemplo: `line_scan_1.1_2026-05-16.pdf`.

### Contenido

El PDF contiene la misma información que el informe [Line Scan Text](#line-scan-text), formateado como un documento A4 con el logotipo de SharKNX, bandas de sección y sombreado de filas alterno. Los números de página y la marca de tiempo de generación aparecen en el pie de página. Ideal para documentar **edificios inteligentes**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-line-scan-pdf.png" width="600" alt="Vista previa del informe PDF de escaneo de línea" />
</div>

**Archivo de muestra:** [sample-line-scan.pdf](../../../../assets/examples/exports/sample-line-scan.pdf)

---

## Device Tables PDF

Exportado desde la Inspect page una vez que se han leído las tablas del dispositivo, a través del botón export en la barra superior. La exportación masiva también está disponible para generar un PDF por dispositivo a partir de la sesión de inspección actual.

### Nombre de archivo

Dispositivo individual:

```
device_tables_{individual_address}_{YYYY-MM-DD}.pdf
```

La exportación masiva produce múltiples archivos con el mismo patrón, guardados en una carpeta elegida por el usuario (escritorio) o compartidos como un lote (móvil).

Ejemplo: `device_tables_1.1.5_2026-05-16.pdf`.

### Secciones

| Sección | Contenido |
|---------|---------|
| **Header + Info** | Dirección física del dispositivo, marca de tiempo de exportación, nombre del proyecto **ETS** (si está cargado) |
| **Communication Objects** | Tabla de asociación expandida con subfilas de dirección de grupo: muestra el número de cada objeto de comunicación, nombre (si está disponible en **ETS**), banderas (flags) y direcciones de grupo vinculadas |
| **Group Address Table** | Entradas RAW de GrAT: índice de ranura (slot index), valor de la dirección de grupo |
| **Device Info** | Campos de Identity, Hardware, Application y Status (los mismos campos que en Line Scan Text) — solo presentes si se realizó un **Read Info** antes de exportar |

Cada sección comienza en una nueva página para que los informes de múltiples secciones se paginen de forma limpia.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-device-tables-pdf.png" width="600" alt="Vista previa del informe PDF de tablas de dispositivo" />
</div>

**Archivo de muestra:** [sample-device-tables.pdf](../../../../assets/examples/exports/sample-device-tables.pdf)

---

## Shark Hunt JSON

Exportado desde la Shark Hunts page (todos los hunts) o desde el action menu de un hunt individual (un solo hunt). El formato es el mismo en ambos casos: una matriz de objetos hunt.

### Nombre de archivo

La aplicación propone un nombre de archivo en el momento de la exportación. La extensión del archivo siempre es `.json`.

### Estructura del archivo

El archivo JSON es una matriz. Cada elemento representa una definición completa de Shark Hunt, incluyendo su nombre, acciones de monitorización y todos los filtros configurados. Esqueleto de ejemplo:

```json
[
  {
    "name": "HVAC Diagnostics",
    "monitor_actions": [
      {
        "name": "All writes to zone 1",
        "filters": { ... }
      }
    ]
  }
]
```

**Sample file:** [sample-shark-hunt.json](../../../../assets/examples/exports/sample-shark-hunt.json)

Una exportación de un solo hunt envuelve ese único hunt en la misma matriz de nivel superior para que el formato de importación sea idéntico independientemente de cuántos hunts contenga el archivo.

### Importación
En la Shark Hunts page, el tune menu → Import Hunts acepta un archivo .json que contiene uno o más objetos hunt. Los hunts importados se añaden a la lista existente; no sobrescriben los hunts existentes.
