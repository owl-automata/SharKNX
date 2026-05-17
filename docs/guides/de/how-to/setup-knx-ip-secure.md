# KNX IP Secure einrichten

KNX IP Secure verschlüsselt die Tunnelverbindung zwischen SharKNX und Ihrem IP-Gateway mittels AES-128 CCM über TCP. Bevor SharKNX eine Verbindung zu einem sicheren Gateway herstellen kann, benötigt die App die passenden Zugangsdaten. Diese Anleitung erklärt, wie Sie diese laden.

Hintergrundinformationen darüber, was KNX IP Secure schützt und wie es funktioniert, finden Sie unter [KNX IP Secure (Konzepte)](../concepts/knx-ip-secure.md).

---

## Was Sie benötigen

Eine der folgenden von der ETS generierten Zugangsdaten-Quellen:

| Format | Herkunft |
|---|---|
| `.knxkeys`-Schlüsselbund-Datei | Export aus der ETS: Projekt $\rightarrow$ Sicherheit $\rightarrow$ Schlüsselbund exportieren |
| `.knxproj`-ETS-Projektdatei | Dieselbe Projektdatei, die auch zum Laden der Gruppenadressen verwendet wird; sie enthält bereits die Geräte-Zugangsdaten. |
| Backbone-Schlüssel (Hex-String) | Zu finden in der ETS unter den IP Secure-Einstellungen der jeweiligen Schnittstelle. |

---

## Schritt 1 — Den Reiter "Sicherheit" öffnen

1. Wechseln Sie auf die Seite **Discovery**.
2. Tippen Sie auf den Reiter **Sicherheit**.

---

## Schritt 2 — Zugangsdaten laden

Es stehen drei Methoden zur Verfügung. Wählen Sie die Methode, die zu Ihren vorliegenden Daten passt:

### Methode A — Eine `.knxkeys`-Schlüsselbund-Datei laden

1. Tippen Sie auf **.knxkeys-Datei laden**.
2. Wählen Sie die `.knxkeys`-Datei aus dem Speicher Ihres Geräts aus.
   - Falls die Datei passwortgeschützt ist, geben Sie das Passwort für den Schlüsselbund bei der Abfrage ein.
3. Es erscheint eine Zusammenfassungskarte, die bestätigt, wie viele Schnittstellen-Zugangsdaten erfolgreich geladen wurden.

### Methode B — Zugangsdaten aus einer ETS-Projektdatei laden

Wenn Sie bereits eine `.knxproj`-Datei geladen oder griffbereit haben:

1. Tippen Sie auf **Aus ETS-Projekt laden**.
2. Wählen Sie die `.knxproj`-Datei aus (oder bestätigen Sie das bereits geladene Projekt).
   - Falls das Projekt passwortgeschützt ist, geben Sie das Projektpasswort bei der Abfrage ein.
3. Die Zugangsdaten werden automatisch aus der Projektdatei extrahiert und geladen.

### Methode C — Einen Backbone-Schlüssel manuell eingeben

1. Tippen Sie auf **Backbone-Schlüssel eingeben**.
2. Fügen Sie den 32-stelligen Hex-Backbone-Schlüssel ein oder tippen Sie ihn manuell ein.
3. Bestätigen Sie die Eingabe. Der Schlüssel wird gespeichert und für jedes Gateway verwendet, das diesen erfordert.

---

## Schritt 3 — Die Gateway-Karte überprüfen

1. Wechseln Sie zum Reiter **Discover** und starten Sie den Suchlauf nach Gateways, oder öffnen Sie den Reiter **Konfig**, falls Ihr Gateway bereits gespeichert ist.
2. Suchen Sie Ihr sicheres Gateway. Auf dessen Karte sollte ein **Schloss-Symbol** zu sehen sein, welches signalisiert, dass KNX IP Secure unterstützt wird.
3. Wenn die Zugangsdaten erfolgreich geladen wurden, wird das Schloss-Symbol ausgefüllt/aktiv dargestellt. Bleibt das Symbol leer oder zeigt die Gateway-Karte eine Warnung bezüglich fehlender Zugangsdaten an, wiederholen Sie Schritt 2 mit der korrekten Datei.

---

## Schritt 4 — Verbindung herstellen

1. Tippen Sie auf **Auswählen** auf der Gateway-Karte, um es als aktives Gateway festzulegen.
2. Starten Sie den Monitor (oder verbinden Sie sich von einer Shark-Hunt-Seite aus). SharKNX nutzt nun automatisch den sicheren TCP-Tunnel.
3. Wenn die Verbindung erfolgreich hergestellt wurde, wird das Verbindungs-Badge grün und die Telegramme laufen ganz normal ein.

Sollte die Verbindung mit einem Sicherheitsfehler (Security Error) fehlschlagen, sind dies die häufigsten Ursachen:
- Falsche Schlüsselbund-Datei (die Zugangsdaten gehören zu einem anderen Gateway).
- Falsches Passwort für den Schlüsselbund oder das ETS-Projekt.
- Der Werkzeugschlüssel (Tool Key) des Gateways wurde in der ETS nach dem Export des Schlüsselbunds neu generiert – exportieren Sie den Schlüsselbund in der ETS erneut und laden Sie ihn neu in die App.

---

## Wichtige Hinweise

- Zugangsdaten, die über eine `.knxkeys`- oder `.knxproj`-Datei geladen wurden, werden sicher auf dem Gerät gespeichert und bleiben auch nach einem App-Neustart erhalten. Sie müssen diese nicht bei jeder Sitzung neu laden.
- Wenn eine `.knxkeys`-Datei auch Werkzeugschlüssel (Tool Keys) für einzelne Geräte enthält (die für administrative Operationen benötigt werden), werden diese in diesem Schritt ebenfalls geladen und stehen auf den Management- und Projektseiten automatisch zur Verfügung.
- Sie können den Verlauf der zuvor geladenen Zugangsdaten-Dateien direkt im Reiter "Sicherheit" einsehen.
- Um einen anderen Schlüsselbund zu verwenden, laden Sie einfach die neue Datei hoch – sie ersetzt die bisherigen Zugangsdaten.
