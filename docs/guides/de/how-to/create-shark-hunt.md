# Einen Shark Hunt erstellen

Ein Shark Hunt ist eine wiederverwendbare Kombination aus Sende-Aktionen und Monitor-Filtern, die als portable Datei gespeichert wird. Diese Anleitung führt Sie durch den fünfstufigen Erstellungs-Assistenten (Wizard) und erklärt, wie Sie die sechs verfügbaren Aktionstypen konfigurieren.

Eine Übersicht darüber, was Shark Hunts genau sind und wie die Übersichtsseite funktioniert, finden Sie unter [Shark Hunts (Konzepte)](../concepts/shark-hunts.md).

> Die App unterstützt bis zu **25 Hunts**. Jeder einzelne Hunt kann bis zu **25 Aktionen** beinhalten.

---

## Der Erstellungs-Assistent (Wizard)

Tippen Sie auf der Hauptseite von "Shark Hunts" auf den **+ FAB** (schwebender Button), um den Assistenten zu öffnen.

Jeder Schritt des Assistenten verfügt über:
- Ein **X-Symbol** (oben links) zum Schließen – die App warnt Sie vor ungespeicherten Änderungen.
- **Zurück / Weiter**-Buttons am unteren Bildschirmrand, um zwischen den Schritten zu navigieren.
- Einen **Speichern-Button** (oben rechts), der erscheint, sobald Sie eine Änderung vornehmen. Damit können Sie Ihren Fortschritt zwischenspeichern und den Assistenten verlassen, um ihn später fertigzustellen.

---

### Schritt 1 — Name und Beschreibung

Geben Sie einen **Namen** für den Hunt ein (Pflichtfeld) sowie eine optionale **Beschreibung**. Aktivieren Sie den Schalter **Als Favorit markieren**, wenn dieser Hunt ganz oben erscheinen soll, wenn Sie auf der Hauptseite nach dem Stern-Symbol filtern.

---

### Schritt 2 — ETS-Projekt

Wählen Sie aus, ob dieser Hunt ein ETS-Projekt verwenden soll:

| Option | Verwendung |
|---|---|
| **Geladenes ETS-Projekt nutzen** | Es ist bereits ein Projekt geladen – der Hunt greift auf dessen Gruppenadressen, Geräte und Gebäudestruktur für die Aktionserstellung und die Monitor-Filter zu. |
| **Projekt laden** | Es ist noch kein Projekt geladen – öffnet die Dateiauswahl, sodass Sie jetzt eine `.knxproj`-Datei importieren können. |
| **Manuelle Eingabe** | Sie haben kein Projekt oder benötigen keines – Gruppenadressen müssen bei der Aktionserstellung manuell eingetippt werden. |

> Die Aktionstypen **Raum-Monitor (Monitor Space)** und **Geräte-Monitor (Monitor Device)** zwingend ein ETS-Projekt voraus. Wenn Sie die Projektauswahl an dieser Stelle überspringen, stehen diese beiden Aktionstypen in Schritt 3 nicht zur Verfügung.

---

### Schritt 3 — Aktionen

Hier bauen Sie den eigentlichen Inhalt des Hunts auf. Tippen Sie auf **Aktion hinzufügen** und wählen Sie einen Aktionstyp aus der Liste. Details zu den einzelnen Typen finden Sie weiter unten unter [Aktionstypen](#aktionstypen).

Erstellte Aktionen werden als Karten dargestellt. Jede Karte bietet folgende Optionen:
- **Bearbeiten** — öffnet die Konfiguration der Aktion erneut.
- **Kopieren** — dupliziert die Aktion (ideal für ähnliche Aktionen mit nur kleinen Abweichungen).
- **Löschen** — entfernt die Aktion aus dem Hunt.

Wiederholen Sie den Vorgang, bis Sie alle gewünschten Aktionen hinzugefügt haben.

---

### Schritt 4 — IP-Gateway (Optional)

Optional können Sie eine feste Gateway-Konfiguration direkt in den Hunt einbetten. Dadurch kann der Empfänger eines geteilten Hunts sofort eine Verbindung aufbauen, ohne das Gateway selbst suchen oder konfigurieren zu müssen – ideal, wenn Sie die Datei an Endkunden oder weniger technikaffine Kollegen zur Ferndiagnose weitergeben.

Wählen Sie aus den bereits erkannten Gateways oder tippen Sie auf **Manuell konfigurieren**, um IP-Adresse und Port direkt einzugeben. Dieser Schritt kann komplett übersprungen werden, wenn kein eingebettetes Gateway benötigt wird.

---

### Schritt 5 — Prüfen und Erstellen

Hier sehen Sie eine Zusammenfassung all Ihrer Auswahlen. Überprüfen Sie alles und tippen Sie auf **Erstellen**, um den Vorgang abzuschließen. Der Hunt erscheint nun als Karte auf der Hauptseite.

---

## Aktionstypen

Jede Aktionskonfiguration erfordert einen **Aktionsnamen** (Pflichtfeld) und eine optionale **Beschreibung**. Der **Haken-FAB** (Bestätigen-Button) wird aktiv, sobald alle Pflichtfelder ausgefüllt sind. Ein Tippen darauf speichert und erstellt die Aktion.

---

### Fixer Befehl (Send Fixed)

Sendet jedes Mal, wenn die Aktionskarte angetippt wird, einen festen Wert an eine bestimmte Gruppenadresse.

1. Geben Sie die Gruppenadresse ein oder tippen Sie auf das **Lupe-Symbol**, um eine Adresse aus dem geladenen ETS-Projekt auszuwählen (der Datenpunkttyp/DPT wird dabei automatisch ausgefüllt).
2. Wählen Sie zwischen **Schreiben (Write)** oder **Lesen (Read)**.
3. Wählen Sie den passenden **DPT-Typ** und den entsprechenden Untertyp aus.
4. Bei Schreibbefehlen (Write): Geben Sie den zu sendenden Wert ein (z. B. Ein, 75%, 21.5°C, Szene 3).
5. Tippen Sie auf den **Haken-FAB**, um die Aktion zu speichern.

**Praxisbeispiele:** Ein Licht umschalten, einen Temperatur-Sollwert vorgeben, eine Szene abrufen oder eine Jalousieposition testen.

---

### Mehrfachbefehl / Sequenz (Send Multiple / Sequence)

Sendet eine Liste von festen Befehlen nacheinander ab, optional mit zeitlichen Verzögerungen (Delays) dazwischen.

1. Tippen Sie auf den **+ Button**, um den ersten Befehl hinzuzufügen – der Befehls-Editor öffnet sich. Geben Sie Gruppenadresse, DPT, Befehlsart (Read/Write) sowie den Wert ein und bestätigen Sie mit dem Haken-FAB.
2. Tippen Sie erneut auf **+**, um weitere Befehle hinzuzufügen (bis zu **15** Befehle pro Sequenz).
3. Jeder Befehl wird als aufklappbare Karte mit DPT und Wert angezeigt.
4. Um eine Verzögerung vor einem Befehl einzufügen: Tippen Sie auf den Untertitel **"Sofort"** auf der Karte und geben Sie die Verzögerung in Sekunden ein (maximal **10 s**). Der nachfolgende Befehl wartet diese Zeit ab, bevor er gesendet wird.
5. Reihenfolge ändern: Halten Sie das **6-Punkte-Symbol (Drag-Handle)** an einer beliebigen Karte gedrückt und ziehen Sie sie an die gewünschte Position.
6. Tippen Sie auf den **Haken-FAB**, um die gesamte Sequenz-Aktion zu speichern.

**Praxisbeispiel:** Szene aufrufen $\rightarrow$ 2 s warten $\rightarrow$ Status abfragen $\rightarrow$ 1 s warten $\rightarrow$ Bestätigung senden.

---

### Variabler Befehl (Send Variable)

Sendet einen Wert, den Sie erst im Moment der Ausführung flexibel festlegen, an eine oder mehrere Gruppenadressen parallel. Perfekt, um verschiedene Werte auf derselben Adresse zu testen oder mehrere zusammengehörige Adressen gleichzeitig zu beschicken.

1. Geben Sie eine Gruppenadresse in das Eingabefeld ein und tippen Sie auf **Hinzufügen**. Wiederholen Sie dies für alle Zieladressen (bis zu **15**).
   - Nutzen Sie die **Projektsuche**, um mehrere Gruppenadressen aus dem geladenen ETS-Projekt gleichzeitig auszuwählen.
2. Alle hinzugefügten Gruppenadressen müssen denselben DPT besitzen. Abweichungen werden auf den Adresskarten farblich hervorgehoben, blockieren die Erstellung aber nicht – beachten Sie jedoch, dass die Busgeräte bei falschen DPTs eventuell nicht reagieren.
3. Tippen Sie auf den **Haken-FAB**, um zu speichern.

Wenn Sie diese Aktion später auf der Hunt-Seite ausführen, öffnet sich ein Menü am unteren Bildschirmrand mit einem für den DPT passenden Steuerelement (z. B. Slider, Dimmer, Farbwähler). Geben Sie den Wert ein und bestätigen Sie, um ihn an alle hinterlegten Zieladressen gleichzeitig zu senden.

**Praxisbeispiele:** Wählen Sie alle Sollwert-Gruppenadressen von Raumthermostaten einer gesamten Etage aus und senden Sie mit einem einzigen Tippen 21 °C, um zu prüfen, ob alle Heizungszonen korrekt reagieren. Oder steuern Sie alle Dimmkanäle eines Raums an und regeln Sie die Helligkeit schrittweise durch, um das Leuchtmittel zu identifizieren, das bei bestimmten Werten flackert.

---

### Benutzerdefinierter Monitor (Custom Monitor)

Erstellt einen erweiterten Filter für eine Monitor-Sitzung, bei dem Sie eine oder mehrere Bedingungen mithilfe von UND- / ODER-Logiken miteinander verknüpfen können.

1. Tippen Sie auf den **+ Button**, um eine Bedingung hinzuzufügen. Es können bis zu **10 Bedingungen** kombiniert werden.
2. Wählen Sie die Art der Bedingung aus:

   | Bedingung | Filter-Funktion |
   |---|---|
   | **Gruppenadresse** | Zeigt nur Telegramme von/an bestimmte Gruppenadressen. Eingabe manuell oder via Projekt. Unterstützt Wildcards (`1/*/*`, `1/*/0`). Aktivieren Sie **Ausschließen**, um den Filter umzukehren (alles anzeigen, außer diesen Adressen). |
   | **Geräteadresse** | Zeigt nur Telegramme von bestimmten Physikalischen Quelladressen. Manuelle Eingabe oder Projektsuche. Unterstützt Wildcards (`1.*.*`). Aktivieren Sie **Ausschließen** für eine Umkehrung des Filters. |
   | **Telegrammtyp** | Filtert nach dem APCI-Typ: Schreiben (Write), Lesen (Read), Antwort (Response) oder jede beliebige Kombination daraus. |
   | **Textsuche** | Zeigt nur Telegramme, deren Gruppenadressname oder Beschreibung einen bestimmten Suchtext enthält. Erfordert ein geladenes ETS-Projekt. |
   | **Zeitstempel** | Zeigt Telegramme vor, nach oder zwischen bestimmten Uhrzeiten. Ideal zum Testen von zeitgesteuerten Automatisierungen. |

3. Nach dem Hinzufügen der Bedingungen legen Sie den **Logik-Operator** fest: **UND** (alle Bedingungen müssen zutreffen) oder **ODER** (mindestens eine Bedingung muss zutreffen).
4. Tippen Sie auf den **Haken-FAB**, um die Monitor-Aktion zu speichern.

**Praxisbeispiele:**
- *Ein verdächtiges Gerät isolieren:* Fügen Sie eine Bedingung "Geräteadresse" für den verdächtigen Sender UND eine Bedingung "Gruppenadresse" für den betroffenen Adressbereich hinzu. Jetzt sehen Sie ausschließlich die Telegramme, die dieses spezifische Gerät an diese Adressen sendet – alles andere wird ausgeblendet.
- *Eine morgendliche Zeitschaltuhr prüfen:* Fügen Sie eine Bedingung "Zeitstempel" (nach 07:00 Uhr) UND eine Bedingung "Telegrammtyp" (nur Schreiben/Write) hinzu. Starten Sie den Monitor am nächsten Morgen und prüfen Sie, ob die Zeitschaltuhr die richtigen Befehle zur exakten Uhrzeit abgesetzt hat.
- *Den eigenen Test-Datenverkehr ausblenden:* Fügen Sie eine Bedingung "Geräteadresse" mit der Option **Ausschließen** für die Physikalische Adresse Ihres Laptops oder Smartphones hinzu. So sehen Sie während Ihrer Tests nur den echten Datenverkehr der Anlage, ohne Ihre eigenen Sende-Befehle im Protokoll zu haben.

---

### Raum-Monitor (Monitor Space)

Erstellt blitzschnell einen Monitor-Filter, der auf einen physischen Raum oder Bereich Ihrer ETS-Gebäudestruktur begrenzt ist. Erfordert ein in Schritt 2 festgelegtes ETS-Projekt.

1. Wählen Sie aus, was überwacht werden soll:
   - **Gruppenadressen** — überwacht alle Gruppenadressen, die Geräten im ausgewählten Raum zugeordnet sind.
   - **Geräte-Sender** — überwacht alle Physikalischen Adressen von Geräten, die sich in diesem Raum befinden.
2. Tippen Sie auf **Raum auswählen** — Ihre ETS-Gebäudestruktur öffnet sich in einem Menü. Wählen Sie ein Stockwerk, einen Raum oder einen beliebigen Bereich (z. B. Küche, Wohnzimmer).
3. Tippen Sie auf den **Haken-FAB**, um zu speichern.

> Aus einer einzigen Raumauswahl können bis zu **750 Adressen** automatisch erfasst werden. Bei sehr großen Bereichen mit extrem vielen Geräten kann dieses Limit erreicht werden.

---

### Geräte-Monitor (Monitor Device)

Erstellt einen Monitor-Filter, der gezielt auf ein oder mehrere spezifische Geräte aus Ihrem ETS-Projekt ausgerichtet ist. Erfordert ein in Schritt 2 festgelegtes ETS-Projekt.

1. Tippen Sie auf **Geräte auswählen** — die Geräteliste Ihres Projekts öffnet sich. Wählen Sie ein oder mehrere Geräte aus.
2. Der Filter überwacht fortan alle Gruppenadressen, die mit den ausgewählten Geräten verknüpft sind.
3. Tippen Sie auf den **Haken-FAB**, um zu speichern.

> Auch hier gilt das Limit von maximal **750 Adressen**. Äußerst nützlich, um die Kommunikation zwischen zwei bestimmten Geräten zu analysieren oder um sämtliche Ausgänge eines Mehrfachaktors zu validieren.

---

## Einen bestehenden Hunt bearbeiten

Tippen Sie auf der Hauptseite auf das **Drei-Punkte-Menü** einer beliebigen Hunt-Karte und wählen Sie **Bearbeiten**. Dadurch wird der Assistent (Wizard) mit allen bestehenden Daten erneut geöffnet. Sie können den Namen ändern, Aktionen hinzufügen oder entfernen, das eingebettete Gateway anpassen oder jede andere Einstellung aktualisieren.

---

## Einen Hunt teilen

Tippen Sie im Drei-Punkte-Menü auf **Teilen**, um den Hunt als JSON-Datei über die Standard-Teilen-Funktion Ihres Geräts (E-Mail, Messenger, Cloud-Speicher) zu versenden. Der Empfänger importiert die Datei auf seiner eigenen Shark-Hunts-Seite über das **Tuning-Symbol $\rightarrow$ Hunts importieren**. Eine exportierte Datei kann wahlweise einen einzelnen oder mehrere Hunts gleichzeitig enthalten.
