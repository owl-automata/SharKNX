# Die Management-Seite

Die Management-Seite konzentriert sich vollständig auf die Diagnose von KNX-Geräten und -Installationen. Sie unterteilt sich in vier Reiter: **Prog. Mode**, **Devices**, **Line Scan** und **Inspect**.

---

## Reiter "Prog. Mode" (Programmiermodus)

In diesem Reiter können Sie den Bus gezielt nach Geräten durchsuchen, bei denen aktuell der Programmiermodus aktiv ist.

Tippen Sie auf den **Radar-FAB** (schwebender Button mit Radar-Symbol), um den Suchlauf zu starten. Die App horcht auf dem Bus nach Telegrammen von Geräten im Programmiermodus und listet diese als Karten auf. Die Scan-Dauer sowie das Ping-Intervall können in den **Scan-Einstellungen** konfiguriert werden (Zahnrad-Symbol → Scan-Einstellungen).

Jede gefundene Gerätekarte verfügt über zwei Schaltflächen:

- **Info prüfen (Check Info)** — Wechselt zum Reiter *Devices* (Geräte) mit bereits vorausgefüllter Physikalischer Adresse des gefundenen Geräts, bereit zum direkten Auslesen der Geräte-Info.
- **Komm.-Info (Comm. Info)** — Wechselt zum Reiter *Inspect*, ebenfalls mit vorausgefüllter Adresse, bereit zum Auslesen der Kommunikationstabellen des Geräts.

Dies ermöglicht es Ihnen, zuerst einen schnellen Gesamtsuchlauf durchzuführen und anschließend ohne Umwege in die tiefergehende Diagnose eines jeden gefundenen Geräts einzusteigen.

---

## Reiter "Devices" (Geräte)

Der Geräte-Reiter ermöglicht Ihnen die Ausführung von Diagnoseaktionen für jede beliebige Physikalische Adresse – unabhängig davon, ob diese zuvor durch einen Scan gefunden oder direkt manuell eingegeben wurde.

### Data Secure-Badge

Am oberen Rand des Reiters zeigt ein Badge an, ob die Geräteschlüssel für KNX Data Secure geladen sind (aus einer `.knxkeys`-Datei im Sicherheits-Reiter der Discovery-Seite). Wenn keine Schlüssel geladen sind, ist das Badge gelb. Wenn Schlüssel geladen sind, färbt es sich blau und zeigt die Anzahl der geschützten Geräte an. Ein Tippen auf das Badge öffnet ein Übersichtsblatt mit Details und einer Verknüpfung zum direkten Laden einer `.knxkeys`-Datei.

### Adresseingabe

Geben Sie eine Physikalische KNX-Adresse in das Eingabefeld ein. Tippen Sie auf das **Lupe-Symbol**, um die Geräte Ihres geladenen ETS-Projekts komfortabel zu durchsuchen und direkt auszuwählen.

### Aktionen

Sobald eine Adresse eingegeben wurde, stehen vier Aktionen zur Verfügung:

| Aktion | Beschreibung |
|---|---|
| **Prüfen (Check)** | Überprüft, ob das Gerät am Bus physikalisch vorhanden ist und antwortet (Ping). |
| **Info auslesen (Read Info)** | Liest detaillierte Geräteinformationen direkt aus dem Speicher des Geräts aus. |
| **Programmiermodus umschalten** | Schaltet den physischen Programmiermodus des Geräts aus der Ferne ein oder aus. |
| **Neustart (Restart)** | Sendet einen Reset-/Neustart-Befehl an das Gerät. |

Die Funktion **Info auslesen** ruft die folgenden Felder vom Gerät ab:
- Gerätedeskriptor (Device Descriptor, z. B. System B)
- Status des Programmiermodus (Ein/Aus)
- Hersteller und Bestellnummer
- Firmware-Version
- Ladestatus und Betriebsstatus (Run State)
- Applikationsversion
- Status der Adress- und Zuordnungstabelle (Assoziationstabelle)
- Maximale APDU-Länge
- Hardware-Typ
- Fehler-Flags und Gerätestatus

---

## Reiter "Line Scan" (Linien-Scan)

Der Linien-Scan-Reiter prüft eine KNX-Buslinie auf alle dort antwortenden Geräte – völlig unabhängig davon, was Ihr ETS-Projekt enthält. Dies ist ideal, um eine Installation zu überprüfen, unerwartete Geräte aufzuspüren oder sich in einem unbekannten Projekt zurechtzufinden.

### Karte "Scan-Einstellungen"

Konfigurieren Sie den Scan vor dem Start:

| Einstellung | Beschreibung |
|---|---|
| **Bereich und Linie** | Der zu scannende KNX-Bereich und die Linie (z. B. `1.1`). Nutzen Sie **Aus Projekt wählen**, um eine Linie direkt aus Ihrem geladenen ETS-Projekt zu übernehmen – dies stellt auch den Medientyp automatisch ein. |
| **Medientyp** | TP (Twin Pair), IP oder IoT. Erforderlich, damit die App den korrekten Adressbereich für die Abfrage wählt. |
| **Bereich (Range)** | Start- und Endadresse innerhalb der Linie (0–255). Grenzen Sie den Bereich ein, um den Scan zu beschleunigen oder gezielt ein bestimmtes Segment zu prüfen. |

Tippen Sie auf den **Scan-FAB**, um den Vorgang zu starten. Der Scan kann jederzeit vorzeitig abgebrochen werden.

### Scan-Ergebnisse

Gefundene Geräte werden als Karten dargestellt. Die Rahmenfarbe der Karte signalisiert den Gerätetyp:

| Farbe | Gerätetyp |
|---|---|
| Blau | KNX-Koppler (Linien-/Bereichskoppler) |
| Rot | Standard-Anwendungsgerät / KNX-Teilnehmer |
| Grün | KNX Secure-Gerät |

Nach Abschluss eines Scans erscheint über der Kartenliste die Schaltfläche **Geräte-Info auslesen**. Ein Tippen darauf liest nacheinander die Geräte-Infos (Hersteller, Seriennummer und weitere Details) für alle gefundenen Geräte ein – ideal, um sich schnell ein Bild von einer Anlage zu machen, die Sie nicht selbst in Betrieb genommen haben.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-line-scan.png" width="320" alt="Reiter Linien-Scan mit gefundenen Gerätekarten inklusive farbcodierten Rahmen und der Schaltfläche Geräte-Info auslesen" />
</div>

### Detailblatt der Gerätekarte

Tippen Sie auf eine beliebige Gerätekarte, um deren Detailblatt zu öffnen. Es enthält:

- Eine Geräte-Info-Karte (ausgefüllt, sofern "Geräte-Info auslesen" bereits ausgeführt wurde).
- Die gleichen vier Diagnoseaktionen wie im Geräte-Reiter: **Prüfen**, **Info auslesen**, **Programmiermodus umschalten**, **Neustart**.
- **Adresse programmieren** — Öffnet eine Unterseite, auf der Sie eine neue Physikalische Adresse vergeben (oder in Ihrem Projekt danach suchen) und diese über zwei Methoden auf das Gerät schreiben können:
  - **Über Programmierknopf** — Wartet bis zu 20 Sekunden darauf, dass das Gerät manuell in den Programmiermodus versetzt wird, und schreibt dann die Adresse. Prüft zudem vorab auf Adresskonflikte innerhalb der realen Installation.
  - **Über Seriennummer** — Wenn Sie die Geräte-Info bereits ausgelesen haben und die Seriennummer vorliegt, wird die Adresse programmiert, ohne dass ein physischer Zugriff auf den Programmierknopf des Geräts erforderlich ist.
- **Kommunikation rekonstruieren** — Wechselt direkt zum Reiter *Inspect*, wobei die Adresse dieses Geräts bereits vorausgefüllt ist.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-device-card.png" width="320" alt="Detailblatt der Linien-Scan-Gerätekarte mit Diagnose-Aktionsknöpfen und der Option Adresse programmieren" />
</div>

---

## Reiter "Inspect" (Analyse & Rekonstruktion)

Der Inspect-Reiter liest die Kommunikationstabellen eines Geräts direkt aus dessen physikalischem Speicher aus. Dadurch wird vollkommen ohne ETS-Projekt rekonstruiert, welche Kommunikationsobjekte existieren, welche Flags sie besitzen und welche Gruppenadressen mit ihnen verknüpft sind. Dies ist der effektivste Weg, um ein unbekanntes Gerät zu verstehen oder ein Gerät in einer fremden Anlage zu überprüfen.

### Ein Gerät auslesen

Geben Sie die Physikalische Adresse eines Geräts in das Eingabefeld ein und tippen Sie auf **Auslesen (Read)**. Ein Fortschrittsbalken zeigt an, welche Operation gerade läuft. Nach Abschluss erscheint eine Sitzungskarte (Session Card) für das Gerät.

Die Rahmenfarbe der Karte signalisiert Erfolg oder Fehlerschlag. Jede Karte zeigt:
- Physikalische Adresse des Geräts
- Gerätedeskriptor (z. B. System B, KNX-Koppler)
- Ob die vollständige Geräte-Info bereits ausgelesen wurde (zeigt in diesem Fall Hersteller und Bestellnummer an)

Eine Schaltfläche **Vollständige Info auslesen** auf jeder Karte stößt ein separates Auslesen der Geräte-Infos an, falls Sie die vollständigen Details wünschen, ohne die anfängliche Rekonstruktion der Kommunikationstabellen zu verlangsamen.

Sitzungskarten sind **persistent** – sie bleiben auch nach einem App-Neustart erhalten. Nutzen Sie die Schaltfläche **Löschen (Clear)** oberhalb der Kartenliste, um alle Sitzungen zu entfernen, wenn Sie Ihre Arbeit beendet haben.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect.png" width="320" alt="Reiter Inspect mit mehreren Sitzungskarten für verschiedene Geräte" />
</div>

### Sitzungs-Detailseite

Tippen Sie auf eine beliebige Sitzungskarte, um deren vollständige Detailseite zu öffnen. Die obere Statusleiste zeigt die Geräteadresse und den Deskriptor, eine **Aktualisieren-Schaltfläche** zum erneuten Auslesen sowie eine **Teilen-Schaltfläche**, um einen umfassenden PDF-Bericht dieser Sitzung zu exportieren und zu teilen.

Die Detailseite ist in drei Reiter unterteilt:

#### Assoziationen (Zuordnungen)

Listet alle aus dem Gerätespeicher ausgelesenen Kommunikationsobjekte auf, die mit Gruppenadressen verknüpft sind:

| Spalte | Beschreibung |
|---|---|
| **Nummer** | Der Index des Kommunikationsobjekts (KO-Nummer). |
| **Flags** | K (Kommunikation), L (Lesen), S (Schreiben), Ü (Übertragen), A (Aktualisieren), I (Initiallesen) – entsprechend den englischen Flags C, R, W, T, U, I. |
| **Größe** | Objektgröße (1 Bit, 1 Byte, 2 Bytes etc.). |
| **Gruppenadressen** | Alle mit diesem spezifischen Objekt verknüpften Gruppenadressen. |

Jede Gruppenadresse ist antippbar. Da der Datenpunkttyp (DPT) allein aus dem Speicher nicht ermittelt werden kann, wird eine Rohwert-Eingabe (Hexadezimal oder Dezimal) zum Senden von Testbefehlen bereitgestellt.

Die Schaltflächen **Als CSV exportieren** und **Als TXT exportieren** sichern die Assoziationsliste ausschließlich für dieses Gerät.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect-associations.png" width="320" alt="Reiter Assoziationen mit Kommunikationsobjekten inklusive Flags, Größe und verknüpften Gruppenadressen" />
</div>

#### Geräte-Info

Zeigt die vollständige Geräte-Info-Karte (dieselben Felder wie die Aktion "Info auslesen" im Geräte-Reiter). Enthält eine Schaltfläche **Info auslesen**, falls noch nicht geschehen, sowie eine Schaltfläche **Alles kopieren**, um alle Felder für den schnellen Austausch mit Kollegen in die Zwischenablage zu kopieren.

#### Adressen

Eine tabellarische Auflistung aller aus der Adresstabelle des Gerätespeichers ausgelesenen Gruppenadressen mit Spalten für Index, 3-stufiges Format, 2-stufiges Format und Hexadezimalwert. Jede Zeile kann einzeln kopiert werden. Die Schaltflächen **Alles kopieren** und **Als CSV exportieren** stehen oberhalb der Tabelle bereit.

---

## Optionen-Menü (Tuning-Symbol)

Das Tuning-Symbol in der oberen Statusleiste bietet zwei schnelle Export-Aktionen für das aktuellste Linien-Scan-Ergebnis:

- **Als Text exportieren** — Generiert einen TXT-Bericht mit Zeitstempel des Scans, verwendetem Gateway, gescanntem Bereich/Linie, Medium und einer Liste der gefundenen Geräte inklusive deren Detailinformationen.
- **Als PDF exportieren** — Exportiert dieselben Inhalte in einem sauberen, professionellen PDF-Format.
