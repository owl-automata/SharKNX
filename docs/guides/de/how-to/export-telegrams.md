# Telegramme exportieren

SharKNX kann die aktuell in der Monitorliste befindlichen Telegramme in eine Datei exportieren. Sie können die einzuschließenden Spalten, die Anzahl der Telegramme, den Stil der Spaltenüberschriften und das Trennzeichen-Format frei wählen. Exportierte Dateien können lokal gespeichert oder direkt aus der App heraus geteilt werden.

---

## Von der Monitor-Seite

1. Starten Sie eine Monitor-Sitzung und lassen Sie Telegramme einlaufen, oder stoppen Sie den Monitor, sobald Sie den benötigten Datenverkehr aufgezeichnet haben.
2. Tippen Sie auf das **Export-Symbol** (oben rechts in der Zeile der Filterleiste), um das Export-Menü zu öffnen.
3. Konfigurieren Sie den Export:

   | Option | Beschreibung |
   |---|---|
   | **Dateiname** | Standardmäßig mit einem Zeitstempel vorausgefüllt. Bearbeiten Sie ihn, um der Datei einen aussagekräftigen Namen zu geben. |
   | **Spalten** | Wählen Sie die einzuschließenden Spalten aus: ID, Zeit, Quelle, Ziel, Name\*, Typ, Wert\*, Rohdaten (\*erfordert ein geladenes ETS-Projekt). |
   | **Anzahl der Telegramme** | Gibt an, wie viele Telegramme exportiert werden sollen (gezählt ab dem neuesten Eintrag). Nutzen Sie dies, um einen großen Zwischenspeicher auf die letzten N Einträge zu begrenzen. |
   | **Spaltenüberschriften einschließen** | Aktivieren Sie dies, um eine Kopfzeile mit den Spaltennamen oben in der CSV-Datei einzufügen. |
   | **Trennzeichen (Delimiter)** | Komma (Standard), Tabulator oder Semikolon. |

4. Tippen Sie auf **Speichern**, um die Datei auf Ihrem Gerät zu sichern, oder auf **Teilen**, um das native Teilen-Menü Ihres Betriebssystems zu öffnen und die Datei direkt per E-Mail, Cloud-Speicher oder an eine andere App zu senden.

---

## Aus dem Shark-Hunt-Monitor

Dasselbe Export-Menü steht Ihnen auch innerhalb einer Monitor-Aktion eines Shark Hunts zur Verfügung. Tippen Sie einfach auf den **Speichern-/Export-Button** in der oberen Statusleiste (dieser wird aktiv, sobald Telegramme aufgezeichnet wurden). Es gelten exakt dieselben Optionen.

---

## Wichtige Hinweise

- Die Spalten **Name** und **Wert** sind nur dann aussagekräftig, wenn ein ETS-Projekt geladen ist. Ohne Projekt bleiben diese Spalten für die meisten Telegramme leer.
- Die Spalte **Rohdaten (Raw)** ist immer verfügbar und enthält die unanalysierten Hexadezimal-Nutzdaten – dies ist der Basis-Wert, den die App bei geladenem Projekt in einen menschenlesbaren Wert übersetzt.
- Der Export erfasst immer genau das, was sich aktuell im Telegramm-Zwischenspeicher (Buffer) befindet. Wenn der Puffer sein Limit erreicht hat (Standard: 2000 Einträge, konfigurierbar unter **Einstellungen $\rightarrow$ Monitor**), wurden ältere Telegramme bereits überschrieben. Exportieren Sie die Daten daher rechtzeitig, bevor der Puffer vollzulaufen droht, wenn Sie eine lange Aufzeichnung benötigen.
- Exportierte Dateien können zur späteren Überprüfung wieder in den Monitor importiert werden. Nutzen Sie hierzu im **Monitor $\rightarrow$ Optionen-Menü (Tuning-Symbol)** die Funktion **CSV importieren**, um eine zuvor exportierte Datei wieder in die Telegrammliste zu laden.
