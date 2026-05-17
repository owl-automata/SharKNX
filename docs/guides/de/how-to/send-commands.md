# KNX-Befehle senden

SharKNX kann sowohl Schreib- als auch Lesebefehle an jede beliebige KNX-Gruppenadresse senden, während der Bus-Monitor aktiv ist. Diese Anleitung beschreibt den Befehls-Editor (Command Composer), alle Bereiche der App, über die Sie ihn aufrufen können, und die Verwendung von Quick-Send-Chips für wiederkehrende Befehle.

---

## Voraussetzungen

- Ein ausgewähltes IP-Gateway und ein laufender Bus-Monitor (siehe [Verbindung zu einem Gateway herstellen](connect-to-gateway.md)).
- Optional ein geladenes ETS-Projekt, damit Gruppenadressnamen und Datenpunkttypen (DPT) automatisch vorausgefüllt werden.

---

## Der Befehls-Editor (Command Composer)

Der Befehls-Editor ist die zentrale Schnittstelle zum Senden von Telegrammen. Er besteht aus vier Feldern:

| Feld | Beschreibung |
|---|---|
| **Gruppenadresse** | Die KNX-Zielgruppenadresse. Geben Sie diese manuell ein (z. B. `1/2/3`) oder tippen Sie auf das Lupe-Symbol, um Ihr geladenes ETS-Projekt zu durchsuchen. |
| **Befehlsart** | **Schreiben (Write)**, um einen Wert auf den Bus zu senden; **Lesen (Read)**, um den aktuellen Status/Wert abzufragen. |
| **DPT** | Der Datenpunkttyp und Untertyp (z. B. DPT 1.001 — Schalten). Wird automatisch ausgefüllt, wenn die Adresse aus den Projektdaten ausgewählt wird. |
| **Wert** | Für Schreibbefehle: Der zu sendende Wert, dargestellt als eine für den jeweiligen DPT optimierte Eingabemaske (Umschalter, Schieberegler, Farbwähler, Nummernfeld etc.). |

Tippen Sie auf **Senden**, um das Telegramm auf den Bus zu übertragen. Es erscheint sofort in der Telegrammliste des Monitors.

---

## Aufrufmöglichkeiten (Entry Points)

### Von der Monitor-Seite (Standardmethode)

1. Starten Sie den Monitor – der grüne Start-FAB verwandelt sich in einen roten **Sende-FAB**.
2. Tippen Sie auf den **Sende-FAB**.
3. Ein Menü öffnet sich am unteren Bildschirmrand. Tippen Sie auf **Neuer Befehl**, um den Befehls-Editor zu öffnen.
4. Füllen Sie die Felder aus und tippen Sie auf **Senden**.

### Quick-Send-Chips

Nachdem Sie einen Befehl gesendet haben, erscheint im unteren Menü ein **Chip** (Schaltfläche), der die Gruppenadresse und den gesendeten Wert anzeigt. Diese Chips bleiben für die Dauer der aktuellen Sitzung erhalten.

- **Tippen Sie auf einen Chip**, um exakt denselben Befehl sofort erneut zu senden, ohne den Editor zu öffnen.
- **Halten Sie einen Chip gedrückt**, um den Befehls-Editor mit bereits vorausgefüllter Gruppenadresse und DPT zu öffnen – ideal, um schnell einen anderen Wert an dieselbe Adresse zu senden.

### Aus einem Telegramm in der Monitorliste

1. Tippen Sie auf eine beliebige Zeile in der Telegrammliste, um deren Detailblatt zu öffnen.
2. Tippen Sie auf **Schreiben** – der Befehls-Editor öffnet sich mit der Gruppenadresse und dem DPT, die aus dem Telegramm übernommen wurden.
3. Geben Sie den gewünschten Wert ein und tippen Sie auf **Senden**.

Das Detailblatt verfügt außerdem über einen **Lesen**-Button, der sofort eine Leseanforderung sendet, ohne vorher den Editor zu öffnen.

### Von der Projektseite — Reiter Gruppenadressen

1. Wechseln Sie auf die Seite **Projekt** $\rightarrow$ Reiter **Gruppenadressen**.
2. Navigieren Sie durch die Baumstruktur und tippen Sie auf eine einzelne Gruppenadresse.
3. Tippen Sie im unteren Menü auf **Schreiben**, um den Befehls-Editor (vorausgefüllt mit Adresse und DPT) zu öffnen, oder auf **Lesen**, um sofort einen Lesebefehl zu senden.

### Von der Projektseite — Reiter Geräte

1. Wechseln Sie auf die Seite **Projekt** $\rightarrow$ Reiter **Geräte**.
2. Klappen Sie ein Gerät auf und tippen Sie auf eine der darunter aufgelisteten Gruppenadressen.
3. Es erscheint dasselbe untere Menü – tippen Sie auf **Schreiben** oder **Lesen**.

### Von der Seite der Kommunikationsobjekte

1. Wechseln Sie auf die Seite **Projekt** $\rightarrow$ Reiter **Geräte**.
2. Tippen Sie auf ein Gerät (oder halten Sie ein Gerät gedrückt, das mit Gruppenadressen verknüpft ist), um dessen Detailblatt zu öffnen.
3. Tippen Sie auf **Kommunikationsobjekte**, um die Objektseite für dieses spezifische Gerät anzuzeigen.
4. Tippen Sie auf eine beliebige Gruppenadresse, die unter einem Kommunikationsobjekt aufgeführt ist – es öffnet sich dasselbe Lese-/Schreib-Menü mit vorausgefüllter Adresse und DPT.

### Vom Inspect-Tab — Assoziationen

Wenn Sie die Kommunikationstabellen eines Geräts im Reiter **Management $\rightarrow$ Inspect** rekonstruiert haben, listet der Unterreiter *Assoziationen* alle im Gerätespeicher gefundenen Gruppenadressen auf.

1. Tippen Sie im Reiter *Assoziationen* auf eine beliebige Gruppenadresse.
2. Da der exakte Datenpunkttyp (DPT) allein aus dem Speicher des Geräts nicht ermittelt werden kann, wird anstelle einer DPT-spezifischen Oberfläche eine **Rohwert-Eingabe** angezeigt. Geben Sie einen Hexadezimal- oder Dezimalwert ein und senden Sie ihn ab.
3. Ein **Lesen**-Button steht ebenfalls bereit, um eine Leseanforderung an diese Adresse zu richten.

---

## Einen Lesebefehl senden

Eine Leseanforderung (Read Request) fordert das Gerät, das aktuell den Status einer Gruppenadresse hält (das "Hören"-Flag bzw. Aktualisieren-Flag besitzt), dazu auf, seinen aktuellen Wert als Antwort auf den Bus zu senden. Das resultierende Antwort-Telegramm (Response) erscheint daraufhin in der Monitorliste. Wenn die App bereits den Bus überwacht, während Sie auf der Projektseite auf **Lesen** tippen, horcht sie etwa eine Sekunde lang gezielt nach einer Antwort für diese Adresse und zeigt das Ergebnis direkt live im unteren Menü an.

---

## Wichtige Hinweise

- Das Senden von Befehlen ist grundsätzlich nur bei laufendem Bus-Monitor möglich. Die einzige Ausnahme bilden die Aktionskarten in den *Shark Hunts* – diese bauen für jeden Hunt eigenständig eine kurze Verbindung auf und senden die Befehle unabhängig.
- Wenn Sie eine **KNX Data Secure**-Gruppenadresse ansteuern möchten, muss zuvor die Physikalische Absenderadresse konfiguriert werden, da das Gerät verschlüsselte Schreibbefehle andernfalls abweist. Siehe hierzu [KNX Data Secure einrichten](setup-knx-data-secure.md).
- Von Ihnen gesendete Befehle erscheinen wie jedes andere Telegramm ganz normal in der Monitorliste. Sie sehen also sofort, ob der Befehl vom Bus mit einem Bestätigungssignal (ACK) quittiert wurde.
