# Die Shark-Hunts-Seite

Auf der Shark-Hunts-Seite können Sie **Shark Hunts** erstellen, verwalten und ausführen. Dabei handelt es sich um wiederverwendbare Sets aus KNX-Sendeaktionen und Monitorfiltern, die als portable JSON-Dateien gespeichert werden. Ein „Hunt“ bietet Ihnen eine dedizierte Seite mit One-Tap-Aktionen (Aktionen per Fingertipp), vorkonfigurierten Filtern und einem optionalen eingebetteten Gateway – perfekt vorbereitet, um sie mit Kollegen oder Kunden zu teilen.

Hintergrundinformationen zum zugrundeliegenden Konzept finden Sie unter [Shark Hunts (Konzepte)](../concepts/shark-hunts.md).

---

## Layout der Hauptseite

Unterhalb der oberen Statusleiste befindet sich eine Text-Filterzeile. Tippen Sie hier, um die Hunt-Karten nach Namen zu filtern. Das **Stern-Symbol** auf der rechten Seite der Zeile filtert die Liste sofort, sodass nur noch Ihre Favoriten angezeigt werden.

Die obere Statusleiste enthält:

- **Hilfe-Button** — Öffnet eine App-interne Referenzseite zum Konzept der Shark Hunts, den Aktionstypen und Beispielen.
- **Tuning-Symbol (Optionen)** — Bietet zwei Aktionen:
  - **Hunts exportieren** — Exportiert alle vorhandenen Hunts in eine einzige JSON-Datei.
  - **Hunts importieren** — Importiert eine JSON-Datei, die einen oder mehrere Hunts enthält.

### Einen Hunt erstellen

Tippen Sie auf den **"+" FAB**, um den fünfstufigen Erstellungs-Assistenten zu öffnen. Eine vollständige Anleitung finden Sie unter [Einen Shark Hunt erstellen](../how-to/create-shark-hunt.md).

### Hunt-Karten

Jeder erstellte Hunt wird als Karte dargestellt. Die Farbe des oberen Kartenrands signalisiert den jeweiligen Typ:

| Rahmenfarbe | Hunt-Typ |
|---|---|
| Grün | Nur Sendeaktionen |
| Blau | Nur Monitoraktionen |
| Rot | Sowohl Sende- als auch Monitoraktionen |

Jede Karte zeigt den Hunt-Namen, die Beschreibung (falls vorhanden) und das Typ-Label. Zudem verfügt sie über:

- **Stern-Symbol** — Als Favorit markieren oder Markierung aufheben.
- **Drei-Punkte-Menü** — Bearbeiten, Exportieren (einzelne JSON), Teilen, Löschen und Info.
  - **Info** öffnet ein Übersichtsblatt mit Name, Typ, Favoritenstatus, Anzahl und Namen der Aktionen sowie den Zeitstempeln für Erstellung und Änderung.

Ein langes Drücken auf eine beliebige Karte aktiviert den Mehrfachauswahl-Modus (Multi-Select), in dem Sie mehrere Hunts gleichzeitig kopieren, exportieren oder löschen können.

Hunt-Karten sind persistent und bleiben auch nach einem App-Neustart erhalten.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-main.png" width="320" alt="Shark-Hunts-Hauptseite mit Hunt-Karten inklusive farbcodierten oberen Rändern und der Filterzeile" />
</div>

---

## Die Hunt-Detailseite

Ein Tippen auf eine Hunt-Karte opens deren dedizierte Seite. Die obere Statusleiste zeigt einen Zurück-Button und ein Filter-Eingabefeld, um innerhalb der Aktionskarten auf dieser Seite zu suchen.

### Die Badge-Zeile (Status-Leiste)

| Badge | Beschreibung |
|---|---|
| **Hunt-Name** | Ein Tippen öffnet das Hunt-Info-Blatt (Name, Typ, Favorit, Anzahl der Aktionen, Zeitstempel). |
| **Verbindungsstatus** | Rot = getrennt, Grün = verbunden. Ein Tippen verbindet oder trennt die Verbindung zum Gateway. |
| **ETS-Projekt** | Zeigt an, ob ein ETS-Projekt geladen ist. Ein Tippen öffnet ein Übersichtsblatt mit Projektdetails (Name, GA-Format, Daten) und einer Schaltfläche zum Laden oder Entladen des Projekts. |
| **Data Secure** | Zeigt den Status des Data Secure-Absenders an. Grau = keine Data Secure-Gruppenadressen geladen; Gelb = Adressen vorhanden, aber keine Absender konfiguriert (tippen zum Konfigurieren); Grün = Absender konfiguriert (tippen zum Überprüfen). |
| **Gateway** | Zeigt die IP-Adresse des ausgewählten Gateways an. Blau = ausgewählt, Grau = keines ausgewählt, Grün = ausgewählt und verbunden. Ein Tippen öffnet ein Übersichtsblatt mit Gateway-Details und einer Schaltfläche zum Aufheben der Auswahl (wenn keine Überwachung aktiv ist). |

### Verbindung herstellen

Tippen Sie auf den **grünen Verbinden-FAB**, um eine Verbindung zum konfigurierten Gateway herstellen. Falls kein Gateway ausgewählt ist, listet ein Pop-up die verfügbaren Optionen auf – einschließlich eines eventuell bei der Erstellung im Hunt eingebetteten Gateways sowie anderer gefundener und manuell konfigurierter Gateways. Sobald die Verbindung steht, wird der FAB rot und zeigt ein Stopp-Symbol zum Trennen der Verbindung.

Alle Aktionskarten werden ausgegraut und sind erst nach erfolgreicher Verbindungsherstellung interaktiv.

---

## Bereich „Sendeaktionen“

Sendeaktionskarten sind im oberen Bereich der Hunt-Seite gruppiert. Ein Tippen auf eine Karte führt diese sofort aus:

- **Feste Aktion (Fixed action)** — Sendet den vorkonfigurierten Wert ohne weitere Abfrage.
- **Mehrfach- / Sequenzaktion (Multiple / Sequence action)** — Sendet alle Befehle nacheinander, unter Berücksichtigung der konfigurierten Verzögerungszeiten dazwischen.
- **Variable Aktion (Variable action)** — Öffnet ein Menü am unteren Bildschirmrand mit einer für den jeweiligen Datenpunkttyp (DPT) passenden Eingabemaske (z. B. Farbregler für RGB, ein Prozentregler für DPT 5.001). Bestätigen Sie den Sendevorgang über den Senden-Button.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Hunt-Detailseite mit Sendeaktionskarten im oberen Bereich und Monitoraktionskarten darunter" />
</div>

---

## Bereich „Monitoraktionen“

Die Monitoraktionskarten sind unterhalb der Sendeaktionen gruppiert. Ein Tippen auf eine Karte öffnet den **Shark-Hunt-Monitor** für diese Aktion – eine Überwachungssitzung, bei der die Filter der Aktion sofort aktiv angewendet werden.

### Der Shark-Hunt-Monitor

Die Seite des Shark-Hunt-Monitors ähnelt der Haupt-[Monitor-Seite](monitor.md), ist jedoch exakt auf den Filter der aktiven Aktion zugeschnitten. Die obere Statusleiste zeigt den Namen des Hunts als Titel und den Namen der Monitoraktion als Untertitel, ergänzt durch eine **Speichern/Exportieren**-Schaltfläche (aktiv, sobald Telegramme erfasst wurden).

#### Die Badge-Zeile (Status-Leiste)

| Badge | Beschreibung |
|---|---|
| **Senden** | Öffnet ein Menü am unteren Bildschirmrand, um einen Befehl zu erstellen und zu senden. Zeigt zudem Schnellsenden-Chips für kürzlich verwendete Befehle; langes Drücken auf einen Chip öffnet den Editor mit vorausgefüllten Feldern. |
| **Filter-Details** | Zeigt die Bedingungen des aktuell aktiven Filters an. |
| **Löschen** | Leert alle Telegramme aus der aktuellen Liste. |
| **Data Secure** | Identisch mit dem Data Secure-Badge der Hunt-Detailseite. |
| **Ansicht** | Sortierung (Neueste zuerst / Älteste zuerst) und Gruppenadressformat. Betrifft neu eingehende Telegramme. |
| **Statistik** | Gesamtzahl der Telegramme, Rate (Telegramme/Sek.), am häufigsten aufgetretene Gruppenadressen, aktivste Quellgeräte und häufigste Telegrammtypen. |
| **Gateway** | Identisch mit dem Gateway-Badge der Hunt-Detailseite. |

Die **Monitor-FABs** funktionieren wie folgt:
- Großer FAB — Grün/Start zum Beginnen der Überwachung, Rot/Stopp zum Beenden.
- Kleiner FAB darüber — Öffnet eine Übersicht aller Monitoraktionen in diesem Hunt, sodass Sie den Filter wechseln können, ohne die Seite verlassen zu müssen. Die aktuell aktive Aktion wird mit einem grünen Punkt gekennzeichnet.

#### Die Telegrammliste

Jede Telegrammzeile zeigt folgende Informationen:
- Physikalische Absenderadresse $\rightarrow$ Ziel-Gruppenadresse
- Gruppenadressname | Wert | Hex-Rohdatenwert (Name und Wert erfordern ein geladenes ETS-Projekt)
- Zeitstempel im Format `HH:MM:SS.ms`

Ein Tippen auf eine Zeile öffnet das Telegramm-Detailblatt mit allen Feldern (Zeit, Quelle, Ziel, Name, Wert, Rohdaten-Payload) und zwei Aktionsschaltflächen – **Lesen** (sendet einen Lesebefehl an die Gruppenadresse) und **Schreiben** (öffnet den Befehls-Editor vorausgefüllt mit Adresse und DPT). Eine dritte Schalfläche, **Plot**, öffnet eine Diagrammansicht mit zwei Reitern: Einem zeitlichen Linienverlauf des Gruppenadresswerts und einem Balkendiagramm der Physikalischen Absenderadressen.

#### Exportieren

Das Export-Menü ermöglicht es Ihnen, die Datei zu benennen (mit einem Zeitstempel vorausgefüllt), die zu exportierenden Spalten auszuwählen (ID, Zeit, Quelle, Ziel, Name, Typ, Wert, Rohdaten), den Umfang des Exports festzulegen, Spaltenüberschriften ein- oder auszuschalten und das Trennzeichen zu wählen (Komma, Tabulator oder Semikolon).
