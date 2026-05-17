# Erste Schritte mit SharKNX

SharKNX ist ein professioneller KNX-Inbetriebbegleiter für Smartphones, Tablets und PCs. Diese Anleitung führt Sie durch den grundlegenden Workflow: Verbindung zu einem KNX-IP-Gateway herstellen, ein ETS-Projekt laden und eine Live-Sitzung im Bus-Monitor starten.

## Voraussetzungen

- Ein Gerät mit Android, iOS, Windows oder macOS 13+
- Ein KNX-IP-Gateway, das im selben IP-Netzwerk wie Ihr Gerät erreichbar ist
- (Empfohlen) Eine ETS-Projektdatei (`.knxproj`) Ihrer Installation

> **Abonnement:** Für die Nutzung von SharKNX ist ein aktives Abonnement erforderlich. Nach der Erstinstallation steht Ihnen eine 2-tägige kostenlose Vorschau ohne Registrierung zur Verfügung. Die Monats- und Jahresabonnements beinhalten eine 14-tägige kostenlose Testphase. Zudem ist eine Lifetime-Lizenz als Einmalkauf erhältlich. Details finden Sie unter [Abonnements & Tarife](reference/subscription-plans.md).

---

## Schritt 1 — KNX-IP-Gateway finden (Discovery)

Die Seite **Discovery** öffnet sich automatisch beim App-Start. Es ist die Registerkarte ganz links in der unteren Navigationsleiste.

1. Tippen Sie auf den **Scan-FAB** (schwebender Aktionsbutton) am unteren Bildschirmrand.  
   Die App sendet KNX-IP-Suchanfragen (Search Requests) in Ihr lokales Netzwerk. Alle antwortenden KNX-IP-Gateways werden als Karten in der Liste angezeigt.

2. Tippen Sie auf der Karte des gewünschten Gateways auf **Auswählen**.  
   Das Gateway wird in den Bereich **Zuletzt ausgewähltes Gateway** oben auf der Seite verschoben und bleibt auch bei einem Neustart der App gespeichert – ein erneuter Scan beim nächsten Start ist nicht nötig.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-discovery.png" width="320" alt="Discovery-Tab mit einer erkannten Gateway-Karte sowie den Buttons Auswählen und Speichern" />
</div>

> **Kein Gateway gefunden?** Stellen Sie sicher, dass sich Ihr Gerät im selben Netzwerksegment wie das Gateway befindet. Bei WLAN-Verbindungen über separate VLANs werden Multicast-Pakete häufig vom Router blockiert. Nutzen Sie in diesem Fall den Tab **Konfig**, um das Gateway manuell per IP-Adresse und Port hinzuzufügen, oder aktivieren Sie **Unicast-Subnetz-Scan erzwingen** in den Discovery-Einstellungen.

> **KNX IP Secure?** Wenn Ihr Gateway KNX IP Secure-Anmeldedaten erfordert, tippen Sie auf die Gateway-Karte und nutzen Sie den Button **Zugangsdaten laden**. Den vollständigen Ablauf finden Sie unter [KNX IP Secure einrichten](how-to/setup-knx-ip-secure.md).

> **Für später speichern:** Tippen Sie auf **Speichern** auf einer Gateway-Karte, um es dauerhaft im Tab **Konfig** zu hinterlegen. Gespeicherte Gateways sind sofort ohne erneuten Suchlauf verfügbar – ideal für wiederkehrende Einsätze auf derselben Baustelle oder Anlage.

---

## Schritt 2 — ETS-Projekt laden

Ein ETS-Projekt liefert SharKNX die Namen der Gruppenadressen, Datenpunkttypen (DPT) und Geräte-Metadaten Ihrer Installation. Ohne Projektdatei werden Telegramme nur als reine Hexadezimalwerte ohne Bezeichnungen oder dekodierte Werte dargestellt.

1. Wechseln Sie auf die Seite **Projekt** (zweiter Tab in der unteren Navigationsleiste).
2. Tippen Sie auf den **Ordner-FAB**, um die Dateiauswahl zu öffnen. Navigieren Sie zu Ihrer `.knxproj`-Datei und wählen Sie diese aus.  
   Wenn Sie bereits Projekte geladen haben, erscheint zuerst ein Verlauf – wählen Sie einen früheren Eintrag oder tippen Sie auf **Durchsuchen**, um eine neue Datei zu öffnen.
3. Warten Sie, bis das Projekt vollständig geladen ist. Die vier Reiter (Gruppenadressen, Geräte, Topologie, Gebäude) werden nun mit Ihren Projektdaten befüllt.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-load-project.png" width="320" alt="Projektseite mit aufgeklapptem Gruppenadressen-Baum nach dem Laden eines ETS-Projekts" />
</div>

> **So kommt die Datei auf Ihr Mobilgerät:** Exportieren Sie Ihr ETS-Projekt von Ihrem PC (`Datei → Projekt exportieren` oder Rechtsklick auf das Projekt in der ETS). Übertragen Sie die `.knxproj`-Datei anschließend auf Ihr Smartphone oder Tablet – z. B. per Messenger (gespeicherte Nachrichten in WhatsApp, Telegram etc.), als E-Mail-Anhang, über einen Cloud-Dienst (Google Drive, iCloud, OneDrive) oder klassisch per USB-Kabel.

> **Passwortgeschützte Projekte** werden voll unterstützt. Die App fragt das Projektpasswort automatisch während des Imports ab.

> **Diesen Schritt überspringen:** Sie können den Bus-Monitor auch ohne Projekt nutzen. Die Telegramme zeigen dann jedoch nur die physikalischen Quelladressen und Ziel-Gruppenadressen mit rohen Hex-Nutzdaten.

---

## Schritt 3 — Bus-Monitor starten

1. Wechseln Sie auf die Seite **Monitor** (vierter Tab in der unteren Navigationsleiste).
2. Tippen Sie auf den grünen **Start-FAB**.
   - Falls noch kein Gateway ausgewählt wurde, öffnet sich eine Auswahl mit Ihren erkannten und gespeicherten Gateways – wählen Sie eines aus, um fortzufahren.
   - Die App verbindet sich mit dem Gateway und beginnt mit der Aufzeichnung der Telegramme.
3. Eintreffende Telegramme werden als Zeilen in der Liste dargestellt. Jede Zeile enthält:
   - Physikalische Quelladresse → Ziel-Gruppenadresse
   - Gruppenadressen-Name und dekodierter Wert *(erfordert geladenes ETS-Projekt)*
   - Rohe Hex-Nutzdaten (Payload)
   - Zeitstempel im Format `HH:MM:SS.ms`

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-monitor-active.png" width="320" alt="Monitor-Seite mit Live-Telegrammen in der Listenansicht" />
</div>

> Tippen Sie auf eine beliebige Telegrammzeile, um deren Details zu öffnen. Hier sehen Sie Quelle, Ziel, den dekodierten Wert und finden Buttons, um direkt einen **Lesebefehl (Read)** oder **Schreibbefehl (Write)** an diese Adresse zu senden.

> **Bildschirm eingeschaltet lassen:** Auf Mobilgeräten stoppt die Aufzeichnung, wenn sich der Bildschirm sperrt. Um dies zu verhindern, ist der Modus "Bildschirm immer an" in den Monitor-Einstellungen standardmäßig aktiviert.

---

## Schritt 4 — KNX-Befehl senden

Bei laufendem Bus-Monitor können Sie Testbefehle senden, ohne die Monitor-Ansicht verlassen zu müssen.

1. Tippen Sie auf den roten **Senden-FAB** (dieser ersetzt den Start-FAB, sobald der Monitor aktiv ist).
2. Tippen Sie im sich öffnenden Menü auf **Neuer Befehl**.
3. Im Befehls-Editor:
   - Geben Sie eine Gruppenadresse ein oder tippen Sie auf das **Lupe-Symbol**, um die Gruppenadressen aus Ihrem geladenen Projekt zu durchsuchen.
   - Wählen Sie zwischen **Schreiben (Write)** oder **Lesen (Read)**.
   - Wählen Sie den passenden Datenpunkttyp (DPT) und Untertyp aus.
   - Geben Sie bei einem Schreibbefehl den zu sendenden Wert ein.
4. Tippen Sie auf **Senden**. Der Befehl wird auf den KNX-Bus übertragen und erscheint sofort live in der Telegrammliste.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-send-command.png" width="320" alt="Befehls-Editor mit Eingabefeld für Gruppenadresse, DPT-Auswahl und Wert-Feld" />
</div>

> **Schnelles Erneutes Senden:** Nach dem Senden eines Befehls erscheint ein kleiner Button (Chip) mit der Adresse und dem Wert direkt neben dem Senden-FAB. Tippen Sie darauf, um den Befehl sofort erneut zu senden, oder halten Sie ihn gedrückt, um den Editor mit den vorausgefüllten Daten zu öffnen.

---

## Nächste Schritte

Sie haben nun eine aktive Monitor-Sitzung, ein ETS-Projekt mit Klarnamen geladen und wissen, wie man Testbefehle sendet. Hier geht es weiter:

| Ziel | Anleitung |
|---|---|
| Gruppenadressen durchsuchen und Befehle direkt aus dem Projektbaum senden | [Projektseite](pages/project.md) |
| Wiederverwendbare Befehls- und Filtersätze erstellen | [Shark Hunts (Konzepte)](concepts/shark-hunts.md) |
| Entschlüsselung für KNX Data Secure Gruppenadressen einrichten | [KNX Data Secure einrichten](how-to/setup-knx-data-secure.md) |
| Eine Buslinie scannen und die Präsenz von Geräten prüfen | [Buslinie scannen](how-to/scan-bus-line.md) |
| Monitor-Sitzung als CSV oder PDF exportieren | [Export-Formate](reference/export-format.md) |
| Firmware-Informationen von Geräten auslesen oder Programmiermodus umschalten | [Geräte prüfen / Diagnose](how-to/inspect-device.md) |
