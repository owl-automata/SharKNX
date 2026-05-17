# Die Monitor-Seite

Die Monitor-Seite bietet eine Live-Sitzung zur KNX-Busüberwachung. Eintreffende Telegramme werden in Echtzeit erfasst und in einer scrollbaren Liste dargestellt. Sie können Telegramme filtern, analysieren, grafisch darstellen und exportieren sowie direkt von dieser Seite aus Befehle an den Bus senden.

---

## Starten und Stoppen

Tippen Sie auf den grünen **Start-FAB** (schwebender Button mit Wiedergabe-Symbol), um eine Überwachungssitzung zu beginnen.

- Wenn kein Gateway ausgewählt ist, erscheint eine Auswahlmaske mit Ihren gefundenen und gespeicherten Gateways. Wählen Sie eines aus, um fortzufahren.
- Die App verbindet sich mit dem Gateway und startet sofort die Telegrammerfassung.
- Während der Monitor läuft, verwandelt sich der FAB in einen roten **Sende-FAB** (siehe [KNX-Befehle senden](#knx-befehle-senden)).

Tippen Sie auf das **Start/Stopp-Badge** in der Badge-Zeile (siehe unten), um den Monitor anzuhalten. Die Telegrammliste bleibt nach dem Stoppen sichtbar – sie wird erst gelöscht, wenn Sie dies explizit veranlassen.

---

## Die Filterleiste

Die Filterleiste ist oberhalb der Telegrammliste fixiert und somit immer sichtbar.

**Text-Filterleiste** — Geben Sie einen beliebigen Text ein, um die sichtbare Telegrammliste zu filtern. Die Suche gleicht Texte mit Gruppenadressnamen, Werten und Physikalischen Adressen ab. Die zugrundeliegende Gesamtliste wird dabei nicht verändert; durch das Leeren des Filters werden wieder alle erfassten Telegramme angezeigt.

**Suchfilter-Symbol** — Öffnet ein Menü am unteren Bildschirmrand mit zwei Reitern: Der eine listet alle Gruppenadressen aus Ihrem geladenen ETS-Projekt auf, der andere alle Geräte. Tippen Sie auf einen Eintrag, um ihn sofort als aktiven Filter anzuwenden. Ideal, um eine bestimmte Gruppenadresse oder ein Gerät ohne Tipparbeit zu isolieren.

**Auto-Scroll-Button** — Wenn diese Option aktiviert ist (Standardeinstellung), springt die Ansicht bei jedem neuen Telegramm automatisch zum neuesten Eintrag ganz unten. Die App erkennt von selbst, wenn Sie manuell in der Liste nach oben scrollen, und pausiert das Auto-Scrollen, bis Sie wieder ganz nach unten zurückkehren. Ein Tippen auf den Button im deaktivierten Zustand springt sofort wieder zum neuesten Telegramm.

**Export-Button** — Öffnet das Export-Menü am unteren Bildschirmrand. Siehe [Telegramme exportieren](#telegramme-exportieren).

---

## Die Badge-Zeile (Status-Leiste)

Eine scrollbare Zeile mit interaktiven Badges (Status-Schaltflächen) ist direkt unterhalb der Filterleiste fixiert. Jedes Badge ist antippbar:

### Start / Stopp
Startet oder stoppt den Bus-Monitor. Gleiche Funktion wie der Start-FAB, bevor der Monitor läuft.

### Löschen (Clear)
Leert die aktuelle Telegrammliste. Der Bus-Monitor läuft im Hintergrund weiter, falls er aktiv war.

### ETS-Projekt
Zeigt an, ob ein ETS-Projekt geladen ist. Ein Tippen öffnet ein Übersichtsblatt mit Projektdetails (Name, Gruppenadressformat, Erstellungs- und Änderungsdatum) sowie einer Schaltfläche zum Entladen des Projekts. Ist kein Projekt geladen, bietet das Menü eine **Projekt laden**-Schaltfläche, die dieselbe Dateiauswahl wie die Projektseite öffnet.

### Data Secure
Spiegelt den Status von KNX Data Secure für die aktuelle Sitzung wider:

| Badge-Status | Bedeutung |
|---|---|
| Grau | Keine Data Secure-Gruppenadressen im geladenen Projekt vorhanden |
| Gelb | Data Secure-Adressen vorhanden, aber die Absenderadressen sind nicht konfiguriert |
| Grün | Data Secure-Adressen vorhanden und Absenderadressen korrekt konfiguriert |

Ein Tippen auf ein gelbes Badge öffnet ein Menü mit einer Verknüpfung zur Konfigurationsseite für Data Secure-Absender. Siehe [KNX Data Secure einrichten](setup-knx-data-secure.md).

### Telegramme
Zeigt die aktuelle Anzahl der erfassten Telegramme an. Ein Tippen öffnet ein Menü mit folgenden Optionen:
- **Filter aufheben** — Entfernt den aktiven Text- oder Suchfilter (wird nur angezeigt, wenn ein Filter aktiv ist).
- **Telegramme löschen** — Leert die gesamte Liste der erfassten Telegramme.
- **Statistik** — Öffnet eine detaillierte Statistik-Ansicht mit folgenden Daten:
  - Gesamtzahl der Telegramme
  - Telegramm-Rate (Telegramme pro Sekunde, berechnet vom ersten bis zum letzten Zeitstempel)
  - Top-Gruppenadressen prozentual am Gesamtaufkommen
  - Top-Physikalische Adressen (Absender) prozentual
  - Häufigste Telegrammarten (Schreiben, Lesen, Antwort etc.) prozentual

### Ansicht (View)
Öffnet die Darstellungsoptionen für die Telegrammliste:
- **Sortierung** — Neueste zuerst (Standard) oder Älteste zuerst.
- **Adressformat** — Legt fest, wie Gruppenadressen dargestellt werden (3-stufig, 2-stufig oder frei). Standardmäßig wird das Format des geladenen ETS-Projekts verwendet. Änderungen betreffen nur neu eingehende Telegramme; bereits sichtbare Einträge werden nicht nachträglich umformatiert.
- **Ansichts-Filter (View Group)** — Leitet zu einer zweiten Menüseite weiter, auf der Sie die sichtbare Liste gezielt nach Gruppenadresse, Physikalischer Adresse, Telegrammtyp oder Priorität filtern können. Nach Auswahl eines Eintrags werden nur noch die übereinstimmenden Telegramme angezeigt.

### Gateway
Zeigt die IP-Adresse des ausgewählten Gateways an. Die Farbe signalisiert den Verbindungsstatus:

| Farbe | Status |
|---|---|
| Grau | Kein Gateway ausgewählt |
| Blau | Gateway ausgewählt, aber nicht verbunden |
| Grün | Ausgewählt und erfolgreich verbunden |

Ein Tippen öffnet ein Detailblatt des Gateways mit einer Schaltfläche **Auswahl aufheben** (nur verfügbar, wenn der Monitor gestoppt ist).

---

## Die Telegrammliste

Jede Zeile in der Liste enthält folgende Informationen auf einen Blick:
- **Physikalische Absenderadresse $\rightarrow$ Ziel-Gruppenadresse**
- **Gruppenadressname** *(erfordert ETS-Projekt)* | **dekodierter Wert** *(erfordert ETS-Projekt)* | **Hex-Rohdaten-Payload**
- **Zeitstempel** im Format `HH:MM:SS.ms`

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-active.png" width="320" alt="Monitor-Seite mit einlaufenden Live-Telegrammen in der Listenansicht" />
</div>

### Das Telegramm-Detailblatt

Tippen Sie auf eine beliebige Zeile, um das Detailblatt für dieses spezifische Telegramm zu öffnen. Es zeigt:

- Zeitstempel
- Physikalische Quelladresse (Absender)
- Ziel-Gruppenadresse
- Gruppenadressname *(falls ETS-Projekt geladen)*
- Dekodierter Wert *(falls ETS-Projekt geladen)*
- Hex-Rohdaten-Payload

Zwei Aktionsschaltflächen stehen zur Verfügung:
- **Lesen (Read)** — Sendet sofort eine Leseanforderung (Read Request) an die Gruppenadresse des Telegramms.
- **Schreiben (Write)** — Öffnet den Befehls-Editor mit bereits vorausgefüllter Gruppenadresse und passendem Datenpunkttyp; geben Sie einfach den gewünschten Wert ein und senden Sie ihn ab.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-telegram-detail.png" width="320" alt="Telegramm-Detailblatt mit Anzeige von Zeit, Quelle, Ziel, Wert sowie den Schaltflächen Lesen/Schreiben/Plot" />
</div>

### Grafische Darstellung (Plot)

Die Schaltfläche **Plot** im Detailblatt öffnet eine umfassende Diagrammansicht mit zwei Reitern für die ausgewählte Gruppenadresse:

- **Reiter Wert** — Ein zeitlicher Linienverlauf (Time Series Chart) aller erfassten Werte für diese Adresse. Nutzen Sie das Auf- und Zuziehen mit zwei Fingern (Pinch-to-Zoom) zum Zoomen, wischen Sie horizontal zum Verschieben und tippen Sie auf einen Datenpunkt, um dessen exakten Wert und Zeitstempel anzuzeigen.
- **Reiter Quellen** — Ein Balkendiagramm der Physikalischen Absenderadressen, die auf dieser Gruppenadresse Telegramme gesendet haben. Äußerst nützlich, um unerwartete Sender aufzuspüren oder "Rauschen" auf dem Bus zu diagnostizieren.

Eine Info-Karte zeigt den exakten Zeitraum an, den die Diagrammdaten abdecken.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-plot.png" width="320" alt="Plot-Ansicht mit einem zeitlichen Linienverlauf des Werts einer Gruppenadresse über einen bestimmten Zeitraum" />
</div>

---

## KNX-Befehle senden

Während der Bus-Monitor aktiv ist, wird der FAB zu einem roten **Sende-FAB**. Ein Tippen darauf öffnet ein unteres Menü mit folgenden Optionen:

- **Neuer Befehl** — Öffnet den Befehls-Editor. Geben Sie eine Gruppenadresse ein (oder durchsuchen Sie das geladene ETS-Projekt), wählen Sie zwischen Schreiben (Write) oder Lesen (Read), bestimmen Sie den Datenpunkttyp sowie Untertyp, tragen Sie den Wert ein und tippen Sie auf **Senden**. Der gesendete Befehl erscheint augenblicklich in der Telegrammliste.
- **Schnellbefehl-Chips** — Direkt unter dem Button für neue Befehle werden interaktive Chips für kürzlich gesendete Telegramme angezeigt. Tippen Sie auf einen Chip, um exakt denselben Befehl sofort erneut zu senden. Halten Sie einen Chip gedrückt, um den Editor mit den vorausgefüllten Feldern dieses Befehls zu öffnen, sodass Sie den Wert vor dem Senden flexibel anpassen können.

---

## Telegramme exportieren

Das Export-Menü am unteren Bildschirmrand (erreichbar über den Export-Button in der Filterleiste oder das Optionen-Menü) ermöglicht es Ihnen, die aktuelle Telegrammliste als CSV-Datei zu speichern oder zu teilen.

Folgende Optionen stehen zur Verfügung:

| Option | Beschreibung |
|---|---|
| **Dateiname** | Editierbar, standardmäßig mit einem aktuellen Zeitstempel vorausgefüllt. |
| **Spalten** | Kontrollkästchen zur Auswahl der zu exportierenden Daten (ID, Zeit, Quelle, Ziel, Name, Typ, Wert, Rohdaten). |
| **Telegrammanzahl** | Bestimmt den Umfang des Exports (z. B. nur die letzten 100 von insgesamt 5.000 erfassten Telegrammen). |
| **Kopfzeile einschließen** | Schaltet die Spaltenüberschriften in der ersten Zeile der CSV-Datei ein oder aus. |
| **Trennzeichen** | Komma (Standard), Tabulator oder Semikolon. |

**Speichern** schreibt die Datei direkt in den lokalen Speicher Ihres Geräts. **Teilen** öffnet das native Teilen-Menü des Betriebssystems, um die Datei direkt an einen Messenger, ein Cloud-Laufwerk oder per E-Mail zu senden.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-export.png" width="320" alt="Export-Menü mit Eingabefeld für den Dateinamen, Kontrollkästchen zur Spaltenauswahl und den Schaltflächen zum Speichern und Teilen" />
</div>

Die vollständige Struktur der CSV-Datei finden Sie unter [Export-Formate](../reference/export-format.md).

---

## Optionen-Menü (Tuning-Symbol)

Das Tuning-Symbol in der oberen Statusleiste bietet zusätzliche erweiterte Aktionen für die Monitor-Seite:

**SharKNX-CSV importieren** — Lädt eine zuvor aus SharKNX exportierte CSV-Datei zurück in die Telegrammliste. Die importierten Telegramme ersetzen die aktuelle Liste vollständig. Die Datei muss exakt dem SharKNX-Exportformat entsprechen.

**Telegramme exportieren** — Identisch mit der Funktion des Export-Buttons in der Filterleiste.

**Aus ETS-XML importieren** — Lädt eine Telegrammaufzeichnungsdatei (XML) aus der ETS-Software. Ideal, um eine in der ETS erstellte Busaufzeichnung direkt auf Ihrem Mobilgerät zu betrachten, zu analysieren oder mit Kollegen zu teilen. Ersetzt die aktuelle Telegrammliste.

**Projektdaten nachträglich zuweisen (Apply project data)** — Nach dem Laden oder Aktualisierung eines ETS-Projekts ordnet diese Funktion die Gruppenadressnamen und Datenpunkttypen des Projekts rückwirkend allen bereits in der Liste befindlichen Telegrammen zu. Der Bus-Monitor muss hierfür gestoppt sein. Nutzen Sie diese Option, wenn Sie erst Telegramme aufgezeichnet und danach das Projekt geladen haben, oder wenn Sie ein aktualisiertes Projekt einspielen und die neuen Bezeichnungen in den bestehenden Daten sehen möchten.
