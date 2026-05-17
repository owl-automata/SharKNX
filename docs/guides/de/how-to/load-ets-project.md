# Ein ETS-Projekt laden

Das Laden einer `.knxproj`-Datei gibt SharKNX Zugriff auf Gruppenadressnamen, Datenpunkttypen (DPT), Geräte-Metadaten und KNX Data Secure-Schlüssel. Ohne ein Projekt zeigt der Bus-Monitor nur rohe Hexadezimalwerte ohne Klarnamen an.

---

## Bevor Sie beginnen

Die `.knxproj`-Datei muss sich bereits auf Ihrem Gerät befinden. Falls das nicht der Fall ist, übertragen Sie diese zuerst:
- Senden Sie die Datei aus der ETS direkt an Ihr Smartphone/Tablet per Messenger-App, E-Mail oder AirDrop.
- Speichern Sie die Datei in einem Cloud-Speicher (iCloud, Google Drive, OneDrive) und öffnen Sie sie von dort aus.
- Übertragen Sie die Datei klassisch per USB-Kabel.

SharKNX unterstützt `.knxproj`-Dateien aus **ETS5 und ETS6**, einschließlich passwortgeschützter Projekte.

---

## Vorgehensweise

1. Wechseln Sie auf die Seite **Projekt** (zweiter Tab in der unteren Navigationsleiste).
2. Tippen Sie auf den **Ordner-FAB** (schwebender Button).
   - Wenn Sie bereits Projekte geladen hatten, öffnet sich eine **Verlaufsliste** (History Sheet). Tippen Sie einfach auf einen Eintrag, um das Projekt sofort wiederzuladen – ein Durchsuchen des Dateisystems ist nicht nötig.
   - Um eine neue Datei zu laden, tippen Sie auf **Durchsuchen** (Browse), um die native Dateiauswahl Ihres Betriebssystems zu öffnen.
3. Wählen Sie Ihre `.knxproj`-Datei aus.
4. Falls das Projekt **passwortgeschützt** ist, geben Sie das Passwort bei der entsprechenden Abfrage ein und bestätigen Sie es.
5. Das Projekt wird geladen. Die Suchleiste, der Button zum Auf- und Zuklappen sowie die vier Reiter (Gruppenadressen, Geräte, Topologie, Gebäude) werden nun aktiv und befüllt.

---

## Was sich nach dem Laden ändert

- Die **Monitor-Seite** und der **Shark-Hunt-Monitor** zeigen ab sofort die Namen der Gruppenadressen sowie menschenlesbare, dekodierte Werte für einlaufende Telegramme an.
- Über die Suchleiste auf der **Projektseite** können Sie alle Gruppenadressen, Geräte und Gebäudestrukturen direkt nach Namen filtern.
- Enthält das Projekt **KNX Data Secure**-Gruppenadressen, erscheint ein Banner unterhalb der Reiter-Leiste. Tippen Sie darauf, um die Absenderadressen zu konfigurieren, bevor Sie sichere Befehle senden. Siehe hierzu [KNX Data Secure einrichten](setup-knx-data-secure.md).

---

## Projekte von anderen Seiten aus laden

Sie müssen nicht zwingend auf die Projektseite wechseln, um ein Projekt zu laden. Das **ETS-Projekt-Badge** auf der Monitor-Seite sowie auf den Shark-Hunt-Seiten bietet einen **Projekt laden**-Button, sofern aktuell kein Projekt aktiv ist. Ein Tippen darauf öffnet direkt dieselbe Verlaufsliste und Dateiauswahl.

---

## Ein Projekt aktualisieren oder ersetzen

SharKNX kann immer nur ein Projekt gleichzeitig verwalten. Um zu einem neueren ETS-Export oder einem anderen Projekt zu wechseln:

1. Tippen Sie erneut auf den **Ordner-FAB** auf der Projektseite (oder an beliebiger anderer Stelle in der App auf das ETS-Projekt-Badge).
2. Wählen Sie die aktualisierte `.knxproj`-Datei aus.
3. Das neue Projekt ersetzt das vorherige sofort.

> Wenn der Bus-Monitor aktiv ist, während Sie ein neues Projekt laden, gilt dieses sofort für alle neu eingehenden Telegramme. Bereits in der Liste befindliche Telegramme behalten die Metadaten des vorherigen Projekts so lange bei, bis die Monitorliste geleert wird.

Um ein Projekt vollständig aus der App zu entfernen, ohne ein neues zu laden, tippen Sie auf der Projektseite auf das **Optionen-Menü (Tuning-Symbol)** und wählen Sie **Projekt entfernen (Unload project)**.

---

## Wichtige Hinweise

- Das Laden eines falschen Projekts (das nicht zur physischen Installation vor Ort passt) führt zu falschen Gruppenadressnamen und fehlerhaft dekodierten Werten im Monitor. Vergewissern Sie sich immer, dass Sie das exakt passende Projekt für die jeweilige Baustelle oder Anlage aktiv haben.
- Die Projektdatei wird einmalig beim Ladevorgang ausgelesen. SharKNX hält keine dauerhafte Verbindung zur ETS-Software und erkennt Änderungen, die Sie nachträglich in der ETS vornehmen, nicht automatisch. Laden Sie die Datei nach Änderungen in der ETS einfach neu in die App.
- SharKNX nimmt niemals Änderungen an der `.knxproj`-Datei selbst vor.
