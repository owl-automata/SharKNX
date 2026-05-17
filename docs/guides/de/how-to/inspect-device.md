# Kommunikationsobjekte eines Geräts auslesen (Inspect)

Der Reiter **Inspect** (Prüfen) auf der Management-Seite liest die Kommunikationstabellen eines Geräts direkt aus dessen Speicher aus. Er rekonstruiert, welche Kommunikationsobjekte existieren, welche Flags gesetzt sind und welche Gruppenadressen mit ihnen verknüpft sind – vollkommen ohne ein ETS-Projekt zu benötigen. Dies ist der zuverlässigste Weg, ein unbekanntes oder fehlerhaft dokumentiertes Gerät zu analysieren.

---

## Voraussetzungen

- Eine aktive Verbindung zu einem KNX-Gateway (siehe [Verbindung zu einem Gateway herstellen](connect-to-gateway.md)).
- Die Physikalische Adresse des Geräts, das Sie auslesen möchten.

---

## Vorgehensweise

1. Wechseln Sie auf die Seite **Management** und öffnen Sie den Reiter **Inspect**.
2. Geben Sie die Physikalische Adresse des Geräts in das Eingabefeld ein.
   - Sie können diesen Reiter auch vorausgefüllt von anderen Stellen erreichen: aus dem Reiter **Prog. Mode** (tippen Sie auf einer Karte auf **Kommunikations-Info**), von einer Gerätekarte aus dem **Linien-Scan** (tippen Sie auf **Kommunikation rekonstruieren**) oder aus jedem detaillierten Geräte-Datenblatt.
3. Tippen Sie auf **Auslesen (Read)**. Ein Fortschrittsbalken zeigt an, welche Operation gerade läuft (Adresstabelle, Assoziationstabelle, Kommunikationsobjekte).
4. Eine Sitzungskarte (Session Card) für das Gerät erscheint. Die Rahmenfarbe signalisiert den Erfolg (Grün) oder ein Fehlschlagen (Rot).

---

## Vollständige Geräteinformationen auslesen

Das Auslesen der Kommunikationstabelle beinhaltet standardmäßig keine detaillierten Geräteinformationen (Hersteller, Firmware-Version etc.). Tippen Sie auf der Sitzungskarte auf **Vollständige Info auslesen**, um diese Details separat abzurufen.

---

## Sitzungsdetails anzeigen

Tippen Sie auf die Sitzungskarte, um die vollständige Detailseite zu öffnen. Die obere Statusleiste enthält ein **Aktualisieren-Symbol**, um das Auslesen erneut zu starten, sowie ein **Teilen-Symbol**, um einen PDF-Bericht für diese Sitzung zu exportieren und zu versenden.

Die Detailseite ist in drei Reiter unterteilt:

### Assoziationen (Associations)

Listet alle Kommunikationsobjekte auf, mit denen mindestens eine Gruppenadresse verknüpft ist:

| Spalte | Beschreibung |
|---|---|
| Nummer | Index des Kommunikationsobjekts |
| Flags | K Kommunikation · L Lesen · S Schreiben · Ü Übertragen · A Aktualisieren · I Initialisieren |
| Größe | Datengröße des Objekts (1 Bit, 1 Byte, 2 Bytes etc.) |
| Gruppenadressen | Mit diesem Objekt verknüpfte Gruppenadressen |

Tippen Sie auf eine beliebige Gruppenadresse, um direkt einen **Lesebefehl (Read)** oder **Schreibbefehl (Write)** an diese zu senden. Da der Datenpunkttyp (DPT) allein aus dem Speicher des Geräts nicht ermittelt werden kann, wird hierbei eine universelle Hex-/Dezimal-Eingabe anstelle einer DPT-spezifischen Benutzeroberfläche verwendet.

Nutzen Sie **CSV exportieren** oder **TXT exportieren**, um die Assoziationsliste dieser Sitzung zu sichern.

### Geräte-Info (Device Info)

Zeigt die vollständige Geräte-Informationskarte an, sofern **Vollständige Info auslesen** ausgeführt wurde. Enthält den Button **Alle kopieren**, um sämtliche Felder in die Zwischenablage einzufügen.

### Adressen (Addresses)

Eine Tabelle aller Gruppenadressen, die in der Adresstabelle im Speicher des Geräts gefunden wurden (aufgeteilt nach Index, 3-stufig, 2-stufig, Hexadezimal). Nutzen Sie **Alle kopieren** oder **CSV exportieren**, um die vollständige Liste zu extrahieren.

---

## Sitzungen verwalten

Sitzungen sind **dauerhaft (persistent)** – sie bleiben auch nach einem App-Neustart so lange erhalten, bis Sie diese aktiv löschen.

- **Löschen** (oberhalb der Kartenliste) — entfernt alle Sitzungen.
- **Exportieren** (oberhalb der Kartenliste) — exportiert alle Sitzungen gesammelt als ein einziges PDF-Dokument.
- **Teilen** (obere Leiste einer Sitzungs-Detailseite) — exportiert und teilt ausschließlich diese eine spezifische Sitzung als PDF.

---

## Wichtige Hinweise

- Ein fehlgeschlagenes Auslesen (roter Rahmen) bedeutet meist, dass das Gerät nicht antwortet, sich in einem Fehlerzustand befindet oder die Physikalische Adresse falsch ist. Nutzen Sie vorab die Funktion **Prüfen** im Reiter "Geräte", um sicherzustellen, dass das Gerät überhaupt auf dem Bus erreichbar ist.
- Falls das Gerät für administrative Operationen (Gerätemanagement) KNX Data Secure Tool-Schlüssel erfordert, laden Sie die entsprechende `.knxkeys`-Datei im Reiter **Discovery $\rightarrow$ Sicherheit**, bevor Sie den Auslesevorgang starten.
