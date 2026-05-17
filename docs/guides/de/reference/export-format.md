# Exportformate

SharKNX kann Daten je nach Quelle in fünf Formaten exportieren:

| Format | Quelle | Erweiterung |
|--------|--------|-----------|
| [Telegramm-CSV](#telegramm-csv) | Monitor, Shark-Hunt-Monitor | `.csv` |
| [Linien-Scan-Text](#linien-scan-text) | Scan-Seite $\rightarrow$ Linien-Scan-Ergebnisse | `.txt` |
| [Linien-Scan-PDF](#linien-scan-pdf) | Scan-Seite $\rightarrow$ Linien-Scan-Ergebnisse | `.pdf` |
| [Gerätetabellen-PDF](#gerätetabellen-pdf) | Inspect-Seite $\rightarrow$ Gerätetabellen | `.pdf` |
| [Shark-Hunt-JSON](#shark-hunt-json) | Shark-Hunts-Seite | `.json` |

Auf Mobilgeräten wird die exportierte Datei über das Teilen-Menü des Betriebssystems bereitgestellt. Auf Desktop-Systemen (Windows, macOS) öffnet sich ein nativer Dialog zum Speichern von Dateien bzw. Ordnern.

---

## Telegramm-CSV

Exportiert von der Monitor-Seite sowie von jeder Shark-Hunt-Monitor-Seite über die Export-/Speichern-Schaltfläche oder das Tune-Menü.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-telegram-sheet.png" width="320" alt="Unteres Export-Menü für Telegramme" />
</div>

### Dateiname

    SharKNX_[Kontext]_YYYY-MM-DD_HHMMSS.csv

`[Kontext]` ist entweder `Monitor` oder der Name des Shark Hunts (bereinigt, maximal 30 Zeichen). Beispiel: `SharKNX_Monitor_2026-05-16_143022.csv`.

### Dateistruktur

Die erste Zeile ist immer ein Identifikationskommentar:

    # SharKNX Export v1

Danach folgt optional eine Kopfzeile und anschließend eine Datenzeile pro Telegramm.

### Benutzerdefinierbare Spalten

Diese Spalten können vor dem Speichern im unteren Export-Menü einzeln aktiviert oder deaktiviert werden:

| Spalte | Kopfzeile | Beschreibung |
|--------|--------|-------------|
| ID | `ID` | Fortlaufende Position des Telegramms in der Liste |
| Zeit | `Time` | Zeitstempel im Format `HH:MM:SS.mm` |
| Quelle | `Source` | Physikalische Adresse des sendenden Geräts |
| Ziel | `Destination` | Gruppenadresse des Telegramms |
| Name | `Name` | Gruppenadressname aus dem ETS-Projekt (leer, wenn kein Projekt geladen ist) |
| Typ | `Type` | APCI-Typ: `Write`, `Read`, `Response` usw. |
| Wert | `Value` | Dekodierter Wert aus dem ETS-Projekt (leer, wenn kein Projekt geladen ist) |
| Rohdaten | `Raw` | Roh-Payload als Hex-String; immer in den Busdaten vorhanden |

### Metadaten-Spalten

Fünf strukturelle Spalten werden **immer angehängt**, unabhängig von der Benutzerauswahl. Sie werden für den Re-Import in SharKNX verwendet:

| Spalte | Typ | Beschreibung |
|--------|------|-------------|
| `_timestampMs` | Integer | Unix-Zeitstempel in Millisekunden |
| `_isGroupAddress` | Boolean | Gibt an, ob das Ziel eine Gruppenadresse ist |
| `_priority` | String | KNX-Prioritätsfeld |
| `_hopCount` | Integer | Hop Count aus dem Telegramm-Frame |
| `_numericValue` | Float | Numerische Darstellung des dekodierten Werts (falls verfügbar) |

### Optionen

| Option | Standard | Beschreibung |
|--------|---------|-------------|
| Trennzeichen | Komma | Feldtrennzeichen: `,`, `;` oder Tabulator |
| Kopfzeilen einfügen | Aktiviert | Schreibt die Spaltennamen als erste Datenzeile |
| Maximale Telegrammanzahl | Alle | Optionales Begrenzen auf die ersten N Zeilen |

### Import

Eine SharKNX-CSV-Datei kann über das Tune-Menü $\rightarrow$ **SharKNX-CSV importieren** erneut in den Monitor importiert werden. Die Datei muss die Kopfzeile `# SharKNX Export v1` enthalten. Beim Import wird die aktuelle Telegrammliste überschrieben.

**Beispieldatei:** [sample-telegrams.csv](../../../../assets/examples/exports/sample-telegrams.csv)

---

## Linien-Scan-Text

Exportiert von der Scan-Seite nach Abschluss eines Linien-Scans über das Utilities-Menü $\rightarrow$ **Als Text exportieren**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-scan-utilities.png" width="320" alt="Utilities-Menü der Scan-Seite mit Exportoptionen" />
</div>

### Dateiname

    line_scan_{bereich.linie}_{YYYY-MM-DD}.txt

Beispiel: `line_scan_1.1_2026-05-16.txt`.

### Dateistruktur

Der Bericht ist in drei Abschnitte unterteilt, die durch gestrichelte Linien getrennt sind.

**Kopfblock**

    Generated     : 2026-05-16 14:30:22
    ETS Project   : My Building
    Gateway       : Secure Tunnel  192.168.2.7:3671  (1.1.0)
    Line          : 1.1
    Medium        : TP
    Range         : 0 - 255
    Devices Found : 12
    Duration      : 38s

**Geräteliste** — kompakte nummerierte Tabelle:

    [1]   1.1.1    MDT SCN-00.02        (0x0900)
    [2]   1.1.5    Siemens 5WG1...      (0xFFFF)  [DataSecure]
    ...

Jede Zeile zeigt: Index, Physikalische Adresse, Modellbezeichnung, Descriptor-Hexwert sowie ein `[DataSecure]`-Kennzeichen, falls der Descriptor `0xFFFF` ist.

**Detaillierte Ergebnisse** — ein Block pro Gerät mit vier Unterabschnitten:

| Unterabschnitt | Felder |
|------------|--------|
| Identität | Descriptor, Geräte-Rolle, Gerätename, DataSecure |
| Hardware | Seriennummer, Hersteller, Bestellinformationen, Firmware-Version, Hardware-Typ, maximale APDU-Länge |
| Anwendung | Ladezustand, Laufzustand, App-Version, Ladezustand der Adresstabelle, Ladezustand der Zuordnungstabelle, Ladezustand der Gruppenobjekttabelle |
| Status | Programmiermodus, Fehlerflags, Gerätesteuerung |

Felder, die nicht gelesen wurden (z. B. wenn **Info lesen** für ein Gerät nicht ausgelöst wurde), werden als `–` angezeigt.

**Beispieldatei:** [sample-line-scan.txt](../../../../assets/examples/exports/sample-line-scan.txt)

---

## Linien-Scan-PDF

Exportiert von der Scan-Seite nach Abschluss eines Linien-Scans über das Utilities-Menü $\rightarrow$ **Als PDF exportieren**.

### Dateiname

    line_scan_{bereich.linie}_{YYYY-MM-DD}.pdf

Beispiel: `line_scan_1.1_2026-05-16.pdf`.

### Inhalt

Das PDF enthält dieselben Informationen wie der Bericht [Linien-Scan-Text](#linien-scan-text), formatiert als A4-Dokument mit SharKNX-Logo, Abschnittsbändern und alternierender Zeilenschattierung. Seitenzahlen und der Erstellungszeitstempel erscheinen in der Fußzeile.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-line-scan-pdf.png" width="600" alt="Vorschau des Linien-Scan-PDF-Berichts" />
</div>

**Beispieldatei:** [sample-line-scan.pdf](../../../../assets/examples/exports/sample-line-scan.pdf)

---

## Gerätetabellen-PDF

Exportiert von der Inspect-Seite, sobald die Gerätetabellen gelesen wurden, über die Export-Schaltfläche in der oberen Leiste. Zusätzlich ist ein Sammel-Export verfügbar, um eine PDF-Datei pro Gerät aus der aktuellen Inspect-Sitzung zu erzeugen.

### Dateiname

Einzelgerät:

    device_tables_{physikalische_adresse}_{YYYY-MM-DD}.pdf

Beim Sammel-Export werden mehrere Dateien mit demselben Muster erzeugt, die in einem vom Benutzer gewählten Ordner gespeichert (Desktop) oder als Stapel geteilt (Mobilgerät) werden.

Beispiel: `device_tables_1.1.5_2026-05-16.pdf`.

### Abschnitte

| Abschnitt | Inhalt |
|---------|---------|
| **Kopfbereich + Informationen** | Geräteadresse, Export-Zeitstempel, Name des ETS-Projekts (falls geladen) |
| **Kommunikationsobjekte** | Erweiterte Zuordnungstabelle mit Unterzeilen für Gruppenadressen — zeigt Nummer des Kommunikationsobjekts, Name (falls aus ETS verfügbar), Flags und verknüpfte Gruppenadressen |
| **Gruppenadresstabelle** | Rohdaten der GrAT-Einträge: Slot-Index, Gruppenadresswert |
| **Geräteinformationen** | Identitäts-, Hardware-, Anwendungs- und Statusfelder (gleiche Felder wie beim Linien-Scan-Text) — nur vorhanden, wenn vor dem Export **Info lesen** ausgeführt wurde |

Jeder Abschnitt beginnt auf einer neuen Seite, sodass mehrteilige Berichte sauber paginiert werden.

<div align="center">
  <img src="../../../../assets/screenshots/guides/reference/export-format/export-format-device-tables-pdf.png" width="600" alt="Vorschau des Gerätetabellen-PDF-Berichts" />
</div>

**Beispieldatei:** [sample-device-tables.pdf](../../../../assets/examples/exports/sample-device-tables.pdf)

---

## Shark-Hunt-JSON

Exportiert von der Shark-Hunts-Seite (alle Hunts) oder aus dem Aktionsmenü eines einzelnen Hunts (einzelner Hunt). Das Format ist in beiden Fällen identisch — ein Array von Hunt-Objekten.

### Dateiname

Die App schlägt beim Export einen Dateinamen vor. Die Dateierweiterung ist immer `.json`.

### Dateistruktur

Die JSON-Datei ist ein Array. Jedes Element repräsentiert eine vollständige Shark-Hunt-Definition einschließlich Name, Monitor-Aktionen und aller konfigurierten Filter. Beispielstruktur:

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

Ein Export eines einzelnen Hunts kapselt diesen ebenfalls in dasselbe Array der obersten Ebene, sodass das Importformat unabhängig von der Anzahl der enthaltenen Hunts identisch bleibt.

**Beispieldatei:** [sample-shark-hunt.json](../../../../assets/examples/exports/sample-shark-hunt.json)

### Import

Auf der Shark-Hunts-Seite akzeptiert das Tune-Menü $\rightarrow$ **Hunts importieren** eine `.json`-Datei mit einem oder mehreren Hunt-Objekten. Die importierten Hunts werden an die bestehende Liste angehängt — vorhandene Hunts werden nicht überschrieben.
