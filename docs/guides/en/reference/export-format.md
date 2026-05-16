# Export Formats

SharKNX can export data in five formats depending on the source:

| Format | Source | Extension |
|--------|--------|-----------|
| [Telegram CSV](#telegram-csv) | Monitor, Shark Hunt Monitor | `.csv` |
| [Line Scan Text](#line-scan-text) | Scan page → Line Scan results | `.txt` |
| [Line Scan PDF](#line-scan-pdf) | Scan page → Line Scan results | `.pdf` |
| [Device Tables PDF](#device-tables-pdf) | Inspect page → device tables | `.pdf` |
| [Shark Hunt JSON](#shark-hunt-json) | Shark Hunts page | `.json` |

On mobile the exported file is offered via the OS share sheet. On desktop (Windows, macOS) a native save-file or save-folder dialog opens.

---

## Telegram CSV

Exported from the Monitor page and from any Shark Hunt Monitor page using the export/save button or the tune menu.

<img src="../../../../assets/screenshots/guides/reference/export-format/export-format-telegram-sheet.png" width="320" alt="Telegram export bottom sheet" />

### Filename

```
SharKNX_[Context]_YYYY-MM-DD_HHMMSS.csv
```

`[Context]` is either `Monitor` or the Shark Hunt name (sanitised, max 30 characters). Example: `SharKNX_Monitor_2026-05-16_143022.csv`.

### File structure

The first line is always an identification comment:

```
# SharKNX Export v1
```

This is followed by an optional header row and then one data row per telegram.

### User-selectable columns

These columns are toggled individually in the export bottom sheet before saving:

| Column | Header | Description |
|--------|--------|-------------|
| ID | `ID` | Sequential position of the telegram in the list |
| Time | `Time` | Timestamp in `HH:MM:SS.mm` format |
| Source | `Source` | Individual address of the sending device |
| Destination | `Destination` | Group address of the telegram |
| Name | `Name` | Group address name from ETS project (empty if no project loaded) |
| Type | `Type` | APCI type: `Write`, `Read`, `Response`, etc. |
| Value | `Value` | Decoded value from ETS project (empty if no project loaded) |
| Raw | `Raw` | Raw payload as hex string; always present in the bus data |

### Metadata columns

Five structural columns are **always appended** regardless of user selection. They are used for round-trip import back into SharKNX:

| Column | Type | Description |
|--------|------|-------------|
| `_timestampMs` | integer | Unix timestamp in milliseconds |
| `_isGroupAddress` | boolean | Whether the destination is a group address |
| `_priority` | string | KNX priority field |
| `_hopCount` | integer | Hop count from the telegram frame |
| `_numericValue` | float | Numeric representation of decoded value (if available) |

### Options

| Option | Default | Description |
|--------|---------|-------------|
| Delimiter | Comma | Field separator: `,`, `;`, or tab |
| Include headers | On | Writes column names as first data row |
| Max telegrams | All | Optionally limit to the first N rows |

### Import

A SharKNX CSV file can be re-imported into the Monitor via the tune menu → **Import SharKNX CSV**. The file must have the `# SharKNX Export v1` header line. Importing overwrites the current telegram list.

**Sample file:** [sample-telegrams.csv](../../../../assets/examples/exports/sample-telegrams.csv)

---

## Line Scan Text

Exported from the Scan page after a line scan completes, via the utilities menu → **Export as Text**.

<img src="../../../../assets/screenshots/guides/reference/export-format/export-format-scan-utilities.png" width="320" alt="Scan page utilities menu showing export options" />

### Filename

```
line_scan_{area.line}_{YYYY-MM-DD}.txt
```

Example: `line_scan_1.1_2026-05-16.txt`.

### File structure

The report is divided into three sections separated by dashed lines.

**Header block**

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

**Device list** — compact numbered table:

```
  [1]   1.1.1    MDT SCN-00.02        (0x0900)
  [2]   1.1.5    Siemens 5WG1...      (0xFFFF)  [DataSecure]
  ...
```

Each row shows: index, individual address, model string, descriptor hex, and a `[DataSecure]` flag if descriptor is `0xFFFF`.

**Detailed results** — one block per device, with four subsections:

| Subsection | Fields |
|------------|--------|
| Identity | Descriptor, Device Role, Device Name, DataSecure |
| Hardware | Serial No., Manufacturer, Order Info, Firmware version, Hardware Type, Max APDU length |
| Application | Load State, Run State, App Version, Address Table load state, Association Table load state, Group Object Table load state |
| Status | Programming Mode, Error Flags, Device Control |

Fields that were not read (e.g. if **Read Info** was not triggered for a device) are shown as `–`.

**Sample file:** [sample-line-scan.txt](../../../../assets/examples/exports/sample-line-scan.txt)

---

## Line Scan PDF

Exported from the Scan page after a line scan completes, via the utilities menu → **Export as PDF**.

### Filename

```
line_scan_{area.line}_{YYYY-MM-DD}.pdf
```

Example: `line_scan_1.1_2026-05-16.pdf`.

### Content

The PDF contains the same information as the [Line Scan Text](#line-scan-text) report, formatted as an A4 document with the SharKNX logo, section bands, and alternating row shading. Page numbers and the generation timestamp appear in the footer.

<img src="../../../../assets/screenshots/guides/reference/export-format/export-format-line-scan-pdf.png" width="600" alt="Line scan PDF report preview" />

**Sample file:** [sample-line-scan.pdf](../../../../assets/examples/exports/sample-line-scan.pdf)

---

## Device Tables PDF

Exported from the Inspect page once device tables have been read, via the export button in the top bar. Bulk export is also available to generate one PDF per device from the current inspect session.

### Filename

Single device:
```
device_tables_{individual_address}_{YYYY-MM-DD}.pdf
```

Bulk export produces multiple files with the same pattern, saved to a user-chosen folder (desktop) or shared as a batch (mobile).

Example: `device_tables_1.1.5_2026-05-16.pdf`.

### Sections

| Section | Content |
|---------|---------|
| **Header + Info** | Device address, export timestamp, ETS project name (if loaded) |
| **Communication Objects** | Association table expanded with group address sub-rows — shows each communication object's number, name (if available from ETS), flags, and linked group addresses |
| **Group Address Table** | Raw GrAT entries: slot index, group address value |
| **Device Info** | Identity, Hardware, Application, and Status fields (same fields as Line Scan Text) — only present if **Read Info** was performed before exporting |

Each section starts on a new page so multi-section reports paginate cleanly.

<img src="../../../../assets/screenshots/guides/reference/export-format/export-format-device-tables-pdf.png" width="600" alt="Device tables PDF report preview" />

**Sample file:** [sample-device-tables.pdf](../../../../assets/examples/exports/sample-device-tables.pdf)

---

## Shark Hunt JSON

Exported from the Shark Hunts page (all hunts) or from an individual hunt's action menu (single hunt). The format is the same in both cases — an array of hunt objects.

### Filename

The app proposes a filename at export time. The file extension is always `.json`.

### File structure

The JSON file is an array. Each element represents one complete Shark Hunt definition, including its name, monitor actions, and all configured filters. Example skeleton:

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

A single-hunt export wraps that one hunt in the same top-level array so the import format is identical regardless of how many hunts the file contains.

**Sample file:** [sample-shark-hunt.json](../../../../assets/examples/exports/sample-shark-hunt.json)

### Import

On the Shark Hunts page, tune menu → **Import Hunts** accepts a `.json` file containing one or more hunt objects. The imported hunts are appended to the existing list — they do not overwrite existing hunts.
